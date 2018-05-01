---
title: "Schema View Mapping"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 3a3bee08-602d-40f8-b62b-e2ffe116d103
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Configuration Manager Schema View Mapping
In Configuration Manager, the names of views and columns are designed to be as close to the SMS Provider Windows Management Instrumentation (WMI) schema as possible. Because the views names and view column names must be valid SQL identifiers, there are some discrepancies between WMI and SQL names. However, in the majority of cases the following rules can be applied to convert a WMI class name to its corresponding SQL Server view:  

-   Replace SMS_ with v_ for the start of the view name.  

-   If a view name is longer than 30 characters, it is truncated.  

-   WMI property names are the same in the SQL Server views for non-inventory or discovery classes.  

 Beyond this, the following class families have a differing nomenclature for their view equivalents:  

## System Inventory Views  
 The syntax for the current inventory group is v_GS*_\<group name>* (for example, v_GS_Tape_Drive).  

 The syntax for the history inventory group is v_HS*_\<group name>*(for example, v_HS_Tape_Drive).  

> [!NOTE]
>  There is no equivalent Extended History view (WMI class SMS_GEH_System*_\<group name>*) because it is implemented as a stored procedure.  

## Custom Architecture Views  
 The syntax for the current groups is v_G*\<resource type number>_\<group name>* (for example, v_G6_VendorData).  

 In the previous example, it is assumed that a new inventory architecture, for example VendingMachine, has been added to the system and assigned the resource type number 6 and VendorData is a inventory group that is associated with the architecture. The resource type number might be related to the resource type name and its group’s classes using the schema information views.  

 The corresponding history inventory classes will use the suffix H in place of G.  

## Discovery Views  
 The views for discovery data differ from their WMI counterparts in that array properties in WMI are represented as separate views. For example, for the System resource, all the scalar properties are contained in the view v_R_System. There are a number of view tables for the array values, such as v_RA_System_IPAddresses and v_RA_System_MACAddresses. The general rules for the syntax of these views are:  

-   Scalar class: v_R*_\<resource type name>*  

-   Array class: v_RA*_\<architecture name>\_\<group name>*  

 Each array property view has just two columns: ResourceID and a column that contains the actual data. For example, for the view v_RA_System_IPAddresses the data column is v_RA_System_IPAddresses. As with inventory groups for the discovery view, column names differ from those of WMI classes. Each column ends with a zero character, ensuring uniqueness with SQL Server reserved words. In general, this is the only difference between the WMI and view column names although there are exceptions.  

 For more information about the classes that Configuration Manager supports, see [Configuration Manager Reference](../../../develop/reference/configuration-manager-reference.md).  

## See Also  
 [About Configuration Manager Schema](../../../develop/core/understand/about-configuration-manager-schema.md)   
 [Configuration Manager Schema Overview](../../../develop/core/understand/configuration-manager-schema-overview.md)   
 [Configuration Manager Schema SQL Views](../../../develop/core/understand/configuration-manager-schema-sql-views.md)   
 [Configuration Manager SQL View Security](../../../develop/core/understand/sql-view-security.md)
