---
title: Asset intelligence views
titleSuffix: Configuration Manager
description: Information about software applications that are in use throughout the Configuration Manager hierarchy.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: a2ab0d62-4053-4a59-8c5c-613604275909
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Asset intelligence views in Configuration Manager

The Asset Intelligence views in Configuration Manager contain information about software applications that are in use throughout the Configuration Manager hierarchy, software license management in the enterprise, Asset Intelligence configuration settings, and so on. The Asset Intelligence information is retrieved from clients only after the specific reporting classes have been enabled. By default, the Asset Intelligence reporting classes are disabled, and until the classes are enabled and Configuration Manager clients collect hardware inventory, these views will not contain any information. Other Asset Intelligence views contain information from the Asset Intelligence catalog, summary information, and product licensing information. There are external dependencies and dependencies within the product that should be considered before implementing Asset Intelligence or using the SQL views.

For information about the Asset Intelligence prerequisites, see [Prerequisites for asset intelligence in Configuration Manager](../../../../core/clients/manage/asset-intelligence/prerequisites-for-asset-intelligence.md) in the Configuration Manager Documentation Library.

For the step-by-step procedure for enabling Asset Intelligence, see [Configuring asset intelligence in Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) in the Configuration Manager Documentation Library.

The following sections provide detailed information about Asset Intelligence views, Asset Intelligence hardware inventory views, and Asset Intelligence status views.

## Asset intelligence views

The Asset Intelligence views are described in this section.

### v_AI_MVLS

Lists the Microsoft Volume Licensing (MVLS) product pools, by **MLSProductPool**, and the product family name, version, effective quantity, and unresolved quantity.
It is unlikely that this view will be joined to other views.
 
### v_AI_NON_MS_LICENSE

Lists the non-Microsoft product license information, including the product name, publisher, version, language, effective quantity, date of purchase, and so on.
It is unlikely that this view will be joined to other views.
 
### v_AIProxy

Lists proxy information for the Asset Intelligence synchronization point, if one is configured.
It is unlikely that this view will be joined to other views.
 
### v_CAL_INSTALLED_SOFTWARE_DATA

Lists information about the installed software applications on Configuration Manager clients found through Asset Intelligence. This view contains the same information as the **v_GS_INSTALLED_SOFTWARE** view, but it limits the columns displayed.
The view can be joined with other views by using the **MachineID** column, which is the same as the **ResourceID** column in other views.
 
### v_CAL_Processor_Count

Lists the number of processors found on Configuration Manager clients. This view uses the same hardware inventory data as the **v_GS_PROCESSOR** view, but it displays only the count for processors on each client.
The view can be joined with other views by using the **MachineID** column, which is the same as the **ResourceID** column in other views.
 
### v_LU_CAL_ProductList

Lists the products, by **SoftwareCode**, that are being tracked for CALs, as well as the software hash, product category, license type, and when the product license was last updated.
The view can be joined to other views by using the **SoftwareCode** column.
 
### v_LU_Category

Lists information about the Asset Intelligence software categories, by category ID and category name, as well as the language ID, description, and whether the category was created locally. The information contained in this view can be displayed and customized from the **Catalog** node in the Configuration Manager console.
The view can be joined to other views by using the **CategoryID** column.
 
### v_LU_Category_Editable

Lists information about the Asset Intelligence software categories, software families, and custom labels, including the category ID, category name, language ID, description, type, whether the category was created locally, and so on. This view contains information that is found in the **v_LU_Category**, **v_LU_Family**, and **v_LU_Tags** views.
It is unlikely that this view will be joined to other views.
 
### v_LU_Family

Lists information about the Asset Intelligence software families, by family ID and family name, as well as language ID, description, and whether the family was created locally. The information contained in this view can be displayed and customized from the **Software Families** node in the Configuration Manager console.
The view can be joined to other views by using the **FamilyID** column.
 
### v_LU_HardwareReadiness

Lists information about the hardware requirements for specific software applications, including product, minimum CPU, minimum RAM, minimum hard disk size, minimum hard disk free space, and more. The information contained in this view can be displayed and customized from the **Hardware Requirements** node in the Configuration Manager console.
It is unlikely that this view will be joined to other views.
 
### v_LU_MSProd

Lists information about the Microsoft products contained in the Asset Intelligence catalog, including part number, family name, product name, version, language, license type, and so on.
It is unlikely that this view will be joined to other views.
 
### v_LU_SoftwareCode

Lists information about the software application codes contained in the Asset Intelligence catalog, as well as the associated software ID and when the software was last updated.
The view can be joined to other Asset Intelligence and hardware inventory views by using the **SoftwareCode** and **SoftwareID** columns.
 
### v_LU_SoftwareHash

Lists information about the software applications contained in the Asset Intelligence catalog, by software property hash, including application name, version, publisher, software ID, and when the software was last updated.
The view can be joined to other Asset Intelligence and Asset Intelligence hardware inventory views by using the **SoftwarePropertiesHash** and **SoftwareID** columns.
 
### v_LU_SoftwareList

Lists information about the software applications contained in the Asset Intelligence catalog, by software ID and name, including the version, publisher, software category ID, software family ID, custom labels, and so on.
The view can be joined to other Asset Intelligence and Asset Intelligence hardware inventory views by using the **SoftwareID**, **CategoryID**, **FamilyID**, **Tag1ID**, **Tag2ID**, and **Tag3ID** columns.
 
### v_LU_SoftwareList_Editable

Lists information about the software applications, by software ID and name, where the software category, software family, or custom label can be configured with items from the custom catalog. The view also provides the software code, software properties hash, publisher, version, category name and ID, family name and ID, custom labels, and so on. The information contained in this view can be displayed and customized from the **All Inventoried Software Titles** node in the Configuration Manager console.
The view can be joined to other Asset Intelligence and Asset Intelligence hardware inventory views by using the **CategoryID**, **FamilyID**, **Tag1ID**, **Tag2ID**, and **Tag3ID** columns.
 
### v_LU_SoftwareList_Local

Lists information about the software applications contained in the Asset Intelligence catalog, by software ID and name that have a custom software category, custom software family, or custom label. The view also provides the version, publisher, category ID, family ID, label ID (tag ID), last updated date, and so on. This view contains the same source data as the **v_LU_SoftwareIdentity_Local_Repl** view.
The view can be joined to other Asset Intelligence and Asset Intelligence hardware inventory views by using the **SoftwareID**, **CategoryID**, **FamilyID**, **Tag1ID**, **Tag2ID**, and **Tag3ID** columns.
 
### v_LU_Tags

Lists information about the Asset Intelligence custom labels, by tag ID and tag name, as well as the language ID and a description. The information contained in this view can be displayed and customized from the **Custom Labels** node in the Configuration Manager console.
The view can be joined to other views by using the **TagID** column, which is the same as the **CategoryID** column in the **v_LU_Category_Editable** view.
 
### v_LU_LicensedProduct

Lists information about the licensed products contained in the Asset Intelligence catalog, by licensed product ID. This includes the family name, the product name, and the version code.
It is unlikely that this view will be joined to other views.

## Asset intelligence hardware inventory views

The Asset Intelligence hardware inventory views contain information that is retrieved from Configuration Manager client computers using hardware inventory. For more information about the hardware inventory views, see [Hardware Inventory Views in Configuration Manager](hardware-inventory-views-configuration-manager.md). The hardware inventory views that contain Asset Intelligence information are described in this section.
 
### v_GS_AUTOSTART_SOFTWARE

Lists information about the applications on Configuration Manager clients that start automatically with the operating system found through Asset Intelligence.
The view can be joined with other views by using the **ResourceID** column.
 
### v_GS_BROWSER_HELPER_OBJECT

Lists information about the browser objects found on Configuration Manager clients through Asset Intelligence. While some browser helper objects are beneficial, most software considered &quot;malware&quot; is in the form of browser helper objects.
The view can be joined with other views by using the **ResourceID** column.
 
### v_GS_INSTALLED_EXECUTABLE

Lists information about the installed software application executables on Configuration Manager clients found through Asset Intelligence.
The view can be joined with other views by using the **ResourceID** column.
 
### v_GS_INSTALLED_SOFTWARE

Lists information about the installed software applications on Configuration Manager clients found through Asset Intelligence.
The view can be joined with other views by using the **ResourceID** column and with Asset Intelligence views by using the **SoftwareCode0** and **SoftwarePropertiesHash0** columns.
 
### v_GS_INSTALLED_SOFTWARE_CATEGORIZED

Lists information about the installed software applications on Configuration Manager clients found through Asset Intelligence. This view contains the information in the **v_GS_INSTALLED_SOFTWARE** view provides additional details about the installed software.
The view can be joined with other views by using the **ResourceID** column and with Asset Intelligence views by using the **SoftwareCode0**, **SoftwarePropertiesHash0**, **FamilyID**, **CategoryID**, and **SoftwareID** columns.
 
### v_GS_INSTALLED_SOFTWARE_MS

Lists information about the installed Microsoft software applications on Configuration Manager clients found through Asset Intelligence.
The view can be joined with other views by using the **ResourceID** column.
 
### v_GS_SOFTWARE_LICENSING_PRODU

Lists software licensing product information for Windows Configuration Manager clients found through Asset Intelligence.
The view can be joined with other views by using the **ResourceID** column.
 
### v_GS_SOFTWARE_LICENSING_SERVICE

Lists software licensing service information for Windows Configuration Manager clients found through Asset Intelligence.
The view can be joined with other views by using the **ResourceID** column.
 
### v_GS_SOFTWARE_SHORTCUT

Lists software shortcut information for Configuration Manager clients found through Asset Intelligence.
The view can be joined with other views by using the **ResourceID** column.
 
### v_GS_SYSTEM_CONSOLE_USAGE

Lists all system console usage information for Configuration Manager clients found through Asset Intelligence by polling the System Security Event Log.
The view can be joined with other views by using the **ResourceID** column.
 
### v_GS_SYSTEM_CONSOLE_USAGE_MAXGROUP

Lists all system console usage information for Configuration Manager clients found through Asset Intelligence by polling the Windows System Security Event Log. This view contains a subset of information from the **v_GS_SYSTEM_CONSOLE_USAGE** view.
The view can be joined with other views by using the **ResourceID** column.
 
### v_GS_SYSTEM_CONSOLE_USER

Lists all system console user information for Configuration Manager clients found through Asset Intelligence by polling the System Security Event Log.
The view can be joined with other views by using the **ResourceID** column.
 
### v_GS_USB_DEVICE

Lists information about the USB devices found on Configuration Manager clients through Asset Intelligence.
The view can be joined with other views by using the **ResourceID** column.

## Asset intelligence status view

The Asset Intelligence status view contains summary information about the software applications on Configuration Manager clients. For more information about status views, see [Status and alert views in Configuration Manager](status-alert-views-configuration-manager.md). The status view that contains Asset Intelligence information is described in this section.
 
### v_INSTALLED_SOFTWARE_DATA_Summary

Lists the count of the installed software applications on Configuration Manager clients found through Asset Intelligence. This view contains the same source information as the **v_GS_INSTALLED_SOFTWARE** view, but it provides summary information instead of listing the individual system resources.
It is unlikely that this view will be joined to other views.

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)  
