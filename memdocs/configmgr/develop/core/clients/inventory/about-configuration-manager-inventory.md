---
title: "About Configuration Manager Inventory"
ms.date: "09/20/2016"
description: "You can use Configuration Manager to collect hardware and software inventory from Configuration Manager clients by enabling the client agents on a site-by-site basis."
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: cba720a8-679c-4b19-9c3b-431680994626
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3


---
# About Configuration Manager Inventory
You can use Configuration Manager to collect hardware and software inventory from Configuration Manager clients by enabling the client agents on a site-by-site basis.  

 When the hardware inventory client agent is enabled for Configuration Manager sites, hardware inventory data gives you system information (such as available disk space, processor type, and operating system) about each computer. When the software inventory client agent is enabled, you can inventory information, such as the specific file types and versions that are present on client computers. The software inventory client agent can also collect information about files that are inventoried on client systems. Configuration Manager software inventory can also collect files, not just details about the files, from client computers. With file collection, you specify a set of files to be copied from clients to the Configuration Manager site server that the clients are assigned to.  

> [!NOTE]
> For more information, see [Introduction to hardware inventory](../../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md).  

## About Collecting Hardware Inventory  
 When it is enabled, the Configuration Manager hardware inventory client agent automatically collects detailed information about the hardware characteristics of clients in a Configuration Manager site. By using this feature, you can collect a wide variety of information about client computers, such as memory, operating system, and peripherals for client computers.  

 The hardware inventory feature collects data from client computers by querying several data stores on client computers, such as the registry and Windows Management Instrumentation (WMI) namespace classes. The hardware inventory client agent does not query for all possible WMI classes, but it does provide the ability to report on approximately 1,500 hardware properties from almost 100 different WMI classes, by default.  

## About Collecting Software Inventory  
 When it is enabled, the Configuration Manager software inventory client agent can collect software inventory data directly from files (such as .exe files) by inventorying the file header information. Configuration Manager can also inventory unknown files — files that do not have detailed information in their file headers. This provides a flexible, easy-to-maintain software inventory method. You can also have Configuration Manager collect copies of files that you specify. You can view software inventory and collected file information for a client by using Resource Explorer.  

## About NOIDMIF and IDMIF Files  
 Management Information Format (MIF) files can be used to extend hardware inventory information that is collected from clients by the Configuration Manager hardware inventory client agent. During hardware inventory, the information that is stored in MIF files is added to the client inventory report and stored in the site database, where you can use the data in the same ways that you use default client inventory data. Two MIF files can be used when performing client hardware inventories: NOIDMIF and IDMIF.  

 By default, NOIDMIF and IDMIF file information is not inventoried by Configuration Manager sites. To enable NOIDMIF and IDMIF file information to be inventoried, NOIDMIF and IDMIF collection must be enabled. You can choose to enable one or both types of MIF file collection for Configuration Manager sites on the **MIF Collection** tab of the hardware inventory client agent properties.  

> [!IMPORTANT]
>  Before you can add information from MIF files to the Configuration Manager database, you must create or import class information for them. For more information, see the sections **To add a new inventory class** and **To import hardware inventory classes** in [How to Extend Hardware Inventory in Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

### NOIDMIF Files  
 Standard MIF files that are used in Configuration Manager hardware inventory are called NOIDMIF files. NOIDMIF files do not contain a unique identifier for the data. Configuration Manager automatically associates NOIDMIF file data with the client that the NOIDMIF file is collected from when reporting inventory information.  

> [!NOTE]
>  NOIDMIF files themselves are not sent to the site server during a client hardware inventory cycle. The information that is contained within the NOIDMIF file is collected and added to the client inventory report.  

 If the classes defined in an inventoried NOIDMIF file do not already exist in the Configuration Manager site database, new inventory class tables are created in the site database to store the inventoried information. Subsequent inventories will inventory the data stored in the NOIDMIF file and update the existing inventory data for the client in the site database. If the NOIDMIF file is removed from the client, all the classes and properties relating to the NOIDMIF file are deleted from the current inventory information for the client in the site database.  

 For NOIDMIF file information to be inventoried by default, the NOIDMIF file must be stored in the following directory on Configuration Manager clients:  

 %*Windir*%\System32\CCM\Inventory\Noidmifs  

### IDMIF Files  
 Custom MIF files, called IDMIF files, can also be used in Configuration Manager hardware inventory. IDMIF files contain a unique ID and are not associated with the computer they are collected from. IDMIF files can be used to collect inventory data about devices that are not Configuration Manager clients; for example, a shared network printer, DVD player, photocopier, or similar equipment that is not associated with a client-specific computer.  

 When IDMIF collection is enabled for a site, IDMIF files are collected only if they are within the size limit that is specified for custom MIF files defined in the **General** tab of the hardware inventory client agent properties.  

> [!IMPORTANT]
>  Because IDMIF files are not associated with a Configuration Manager client, they are collected by the hardware inventory client agent and sent to the site server along with the client hardware inventory report. Depending on the maximum custom MIF size specified for the site, IDMIF collection might cause increased network bandwidth usage during client inventories and should be planned for before enabling IDMIF file collection.  

 IDMIF files are identical to NOIDMIF files, with these exceptions:  

- IDMIF files must have a delta header that provides architecture, and a unique ID. NOIDMIF files are automatically given a similar header by the system during processing on the client.  

- IDMIF files must include a top-level group with the same class as the architecture being added or changed, and that group must include at least one property.  

- Like NOIDMIF files, IDMIF files have key properties that must be unique. Any class that has more than one instance must have at least one key property defined, or subsequent instances overwrite previous instances.  

- Removing IDMIF files from clients does not cause the associated data in the site database to be deleted during subsequent hardware inventories.  

- IDMIF file information is not added to client inventory reports and sent as MIF files across the network to be processed at the site server.  

  For IDMIF file information to be inventoried by default, the IDMIF file must be stored in the following directory on Configuration Manager clients:  

  %*Windir*%\System32\CCM\Inventory\Idmifs  

## See Also  
 [Configuration Manager Software Development Kit](../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
[Initiate Asset Intelligence synchronization](../asset-intelligence/how-to-initiate-a-synchronization.md)
