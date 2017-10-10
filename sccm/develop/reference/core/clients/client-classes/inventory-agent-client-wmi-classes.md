---
title: "Inventory Agent Client WMI Classes"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 244dda2b-da12-4618-81f2-79e7f3306b31searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Inventory Agent Client WMI Classes
In System Center Configuration Manager, the inventory client agent classes can be broken into three categories:  

-   Inventory client agent settings  

-   Inventory collection  

-   Report state Configuration Manager inventory provider  

 If the IDMIF class name is more than 32 characters, the IDMIF is collected on the client, but the data is not written to the SQL Server database.  

## Inventory Agent Settings  
 These classes define what an inventory client agent collects and how the collection set should be reported.  

|Class|Description|  
|-----------|-----------------|  
|[CollectableFileItem Client WMI Class](../../../../../develop/reference/core/clients/client-classes/collectablefileitem-client-wmi-class.md)|Defines a file collection query.|  
|[FileCollectionAction Client WMI Class](../../../../../develop/reference/core/clients/client-classes/filecollectionaction-client-wmi-class.md)|Defines a file collection set for reporting, such as software file collection or IDMIF collection.|  
|[InventoryAction Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventoryaction-client-wmi-class.md)|Defines an inventory collection set for reporting, such as discovery, hardware inventory, software inventory, software file collection, or IDMIF collection.|  
|[InventoryDataContext Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventorydatacontext-client-wmi-class.md)|Defines an optional context qualifier for a class query.|  
|[InventoryDataItem Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventorydataitem-client-wmi-class.md)|Defines an inventory class property query to be collected for a particular inventory action.|  

## Inventory Collection and Report State  
 These classes are used to track the current state of inventory collection and reporting. The inventory client agent generates these class instances for each type of inventory report.  

|Class|Description|  
|-----------|-----------------|  
|[InventoryActionStatus Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventoryactionstatus-client-wmi-class.md)|Saves the state of each inventory action.|  

## SMS Inventory Provider Classes  
 These classes are defined by Configuration Manager-supplied instance providers and extend inventory collection beyond the standard Windows Management Instrumentation (WMI) providers. In general, these classes expose additional system data through WMI for inventory collection.  

|Class|Description|  
|-----------|-----------------|  
|[FileSystemFile Client WMI Class](../../../../../develop/reference/core/clients/client-classes/filesystemfile-client-wmi-class.md)|Allows the querying of files based on various criteria.|  
|[SMS_MIFGroup Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_mifgroup-client-wmi-class.md)|A dynamic instance provider class that allows WMI reporting of Management Information Format (MIF) files that extend the client inventory.|  
|[NEW : SMS_Windows8Application Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_windows8application-client-wmi-class.md)|A client Windows Management Instrumentation (WMI) class that defines an application.|  
|[SMS_Windows8ApplicationUserInfo Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_windows8applicationuserinfo-client-wmi-class.md)|A client Windows Management Instrumentation (WMI) class that defines user information of an application.|  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).
