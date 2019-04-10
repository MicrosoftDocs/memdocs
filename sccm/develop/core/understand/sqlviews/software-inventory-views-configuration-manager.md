---
title: Software Inventory Views in Configuration Manager
TOCTitle: Software Inventory Views in Configuration Manager
ms:assetid: b3f0c153-cd0c-4dab-9494-2b1d565ccc11
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn581987(v=TechNet.10)
ms:contentKeyID: 60772052
ms.prod: "configuration-manager"
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/30/2019
mtps_version: v=TechNet.10
---

# Software Inventory Views in Configuration Manager

The Configuration Manager software inventory views contain information about the files and their associated products that are found on Configuration Manager clients during software inventory scanning. Software inventory, by default, will scan for all executable file types (\*.exe) on clients. The software inventory options are configured for the site and will determine which files are inventoried and how much information is collected about each. For more information about configuring software inventory, see [How to Configure Software Inventory in Configuration Manager](https://docs.microsoft.com/en-us/previous-versions/system-center/system-center-2012-R2/hh509028(v%3dtechnet.10)) in the Configuration Manager Documentation Library.

## Software Inventory View Schema

There is not a specific software inventory schema view, but the following query joins the **v\_GS\_SoftwareProduct** and **v\_FullCollectionMembership** views to generate the software inventory view schema by product name for the All Systems collection:

```
SELECT MIN(PRD.ProductID) AS ProductID, PRD.ProductName,

PRD.ProductVersion, COUNT(DISTINCT PRD.ResourceID) AS 'Count'

FROM v\_GS\_SoftwareProduct PRD INNER JOIN v\_FullCollectionMembership FCM

ON PRD.ResourceID = FCM.ResourceID

WHERE FCM.CollectionID = 'SMS00001'

GROUP BY PRD.ProductName, PRD.ProductVersion

ORDER BY PRD.ProductName
```

## Software Inventory Views

Some of the software inventory views created in Configuration Manager store system data, and others contain general product and file data. As a general rule, view names that start with **v\_GS** contain data for Configuration Manager clients and can be joined to other views that contain system data by using the **ResourceID** for that client. Software inventory views that start with **v\_** contain file and product data, but it is not specific to individual computers. The software inventory views are described in this section.

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

## See Also

[SQL Server Views in Configuration Manager](sql-server-views-configuration-manager.md)  

