---
title: Software inventory views
titleSuffix: Configuration Manager
description: Information about the files and their associated products that are found on Configuration Manager clients during software inventory scanning.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual


ms.assetid: 65066949-cce6-4202-b8e7-f4e1014ee470
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Software inventory views in Configuration Manager

The Configuration Manager software inventory views contain information about the files and their associated products that are found on Configuration Manager clients during software inventory scanning. Software inventory, by default, will scan for all executable file types (\*.exe) on clients. The software inventory options are configured for the site and will determine which files are inventoried and how much information is collected about each. For more information, see [How to configure software inventory](../../../../core/clients/manage/inventory/configure-software-inventory.md) in the Configuration Manager Documentation Library.

## Software inventory view schema

There is not a specific software inventory schema view, but the following query joins the **v_GS_SoftwareProduct** and **v_FullCollectionMembership** views to generate the software inventory view schema by product name for the All Systems collection:

```
SELECT MIN(PRD.ProductID) AS ProductID, PRD.ProductName,

PRD.ProductVersion, COUNT(DISTINCT PRD.ResourceID) AS 'Count'

FROM v_GS_SoftwareProduct PRD INNER JOIN v_FullCollectionMembership FCM

ON PRD.ResourceID = FCM.ResourceID

WHERE FCM.CollectionID = 'SMS00001'

GROUP BY PRD.ProductName, PRD.ProductVersion

ORDER BY PRD.ProductName
```

## Software inventory views

Some of the software inventory views created in Configuration Manager store system data, and others contain general product and file data. As a general rule, view names that start with **v_GS** contain data for Configuration Manager clients and can be joined to other views that contain system data by using the **ResourceID** for that client. Software inventory views that start with **v_** contain file and product data, but it is not specific to individual computers. The software inventory views are described in this section.

### v_GS_CollectedFile

Lists the files collected by software inventory on each Configuration Manager client.
The view can be joined to other views by using the **ResourceID** column.

### v_GS_LastSoftwareScan

Lists the last time each Configuration Manager client was scanned for software inventory.
The view can be joined to other views by using the **ResourceID** column.

### v_GS_Mapped_Add_Remove_Programs

Lists the software applications on each Configuration Manager client that is mapped to list of installed software in Windows Control Panel.
The view can be joined to other views by using the **ResourceID** column.

### v_GS_SoftwareFile

Lists the files and associated product IDs on each Configuration Manager client.
The view can be joined to other views by using the **ResourceID** column.

### v_GS_SoftwareProduct

Lists the products found on each Configuration Manager client.
The view can be joined to other views by using the **ResourceID** column.

### v_GS_UnknownFile

Lists the files that are not associated with an identified product, on each Configuration Manager client.
The view can be joined to other views by using the **ResourceID** column.

### v_ProductFileInfo

Lists all of the distinct files, by file ID, that have been inventoried in the site, including file name, description, file size, file version, and so on.
The view can be joined to other views by using the **FileID** column.

### v_SoftwareFile

Lists all of the distinct files, by file ID, that have been inventoried in the site, including file name, file version, description, file size, and associated product.
The view can be joined to other views by using the **FileID** and **ProductID** columns.

### v_SoftwareProduct

Lists all of the distinct software products that have been inventoried in the site.
The view can be joined to other views by using the **ProductID** column.

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)  

