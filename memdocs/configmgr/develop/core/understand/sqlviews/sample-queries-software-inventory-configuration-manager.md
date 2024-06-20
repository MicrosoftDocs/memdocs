---
title: Sample queries for software inventory
titleSuffix: Configuration Manager
description: Sample queries that show how software inventory views can be joined to other views to retrieve specific data.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual


ms.assetid: baffc7d9-86a8-4e36-8230-ea4da8cf1f87
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Sample queries for software inventory in Configuration Manager

The following sample queries demonstrate how the Configuration Manager software inventory views can be joined to other views to retrieve specific data. The software inventory views are typically joined to other views by using the **ProductID**, **FileID**, and **ResourceID** columns.

## Joining software inventory views

The following query lists all software files for the Configuration Manager product that have been inventoried on Configuration Manager clients. The **v_GS_SoftwareProduct** and **v_GS_SoftwareFile** views are joined by using the **ProductID** columns.

```sql
    SELECT DISTINCT SF.FileName, SF.FileDescription, SF.FileVersion 
    FROM v_GS_SoftwareProduct SP INNER JOIN v_GS_SoftwareFile SF 
    ��ON SP.ProductID = SF.ProductId 
    WHERE SP.ProductName = 'Configuration Manager' 
    ORDER BY SF.FileName 
```

## Joining software inventory and discovery views

The following query lists all inventoried products and the associated files for a computer with the NetBIOS name of COMPUTER1. The **v_R_System** and **v_GS_SoftwareProduct** views are joined by using the **ResourceID** column, and the **v_GS_SoftwareProduct** and **v_GS_SoftwareFile** views are joined by using the **ProductID** columns.

```sql
    SELECT DISTINCT SP.ProductName, SF.FileName 
    FROM v_R_System SYS INNER JOIN v_GS_SoftwareProduct SP 
    ��ON SYS.ResourceID = SP.ResourceID INNER JOIN v_GS_SoftwareFile SF 
    ��ON SP.ProductID = SF.ProductId 
    WHERE SYS.Netbios_Name0 = 'COMPUTER1' 
    ORDER BY SP.ProductName 
```

## Joining software inventory, discovery, and hardware inventory views

The following query lists all computers that have Microsoft Office installed and have less than 1 GB of free space on the local C drive. The **v_GS_SoftwareFile** and **v_SoftwareProduct** views are joined by the **ProductID** column, and the **v_GS_LOGICAL_DISK** and **v_R_System** views are joined to **v_GS_SoftwareFile** by using the **ResourceID** columns.

```sql
    SELECT DISTINCT SYS.Netbios_Name0, SYS.User_Domain0, LD.FreeSpace0 
    FROM v_GS_SoftwareFile SF INNER JOIN v_SoftwareProduct SP 
    ��ON SF.ProductId = SP.ProductID 
    ��INNER JOIN v_GS_LOGICAL_DISK LD 
    ��ON SF.ResourceID = LD.ResourceID 
    ��INNER JOIN v_R_System SYS 
    ��ON SF.ResourceID = SYS.ResourceID 
    WHERE (LD.Description0 = 'local Fixed Disk') 
    ��AND (SP.ProductName LIKE 'Microsoft Office%') 
    ��AND (LD.FreeSpace0 < 1000) 
    ��AND (LD.DeviceID0 = 'C:') 
```

## Joining software inventory, discovery, and software metering views

The following query lists all files that have been metered through software metering rules and sorted first by NetBIOS name, and then by product name, and then by file name. The **v_GS_SoftwareProduct** and **v_MeteredFiles** views are joined by the **ProductID** column, and the **v_GS_SoftwareProduct** and **v_R_System** views are joined by using the **ResourceID** columns.

```sql
    SELECT SYS.Netbios_Name0, SP.ProductName, SP.ProductVersion, 
    ��MF.FileName, MF.MeteredFileVersion 
    FROM v_GS_SoftwareProduct SP INNER JOIN v_MeteredFiles MF 
    ��ON SP.ProductID = MF.MeteredProductID INNER JOIN v_R_System SYS 
    ��ON SP.ResourceID = SYS.ResourceID 
    ORDER BY SYS.Netbios_Name0, SP.ProductName, MF.FileName 
```

## See also

[Software inventory views in Configuration Manager](software-inventory-views-configuration-manager.md)
