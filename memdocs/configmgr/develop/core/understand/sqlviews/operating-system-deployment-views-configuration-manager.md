---
title: Operating system deployment views
titleSuffix: Configuration Manager
description: Information about boot image packages, computer association state migrations, and operating system image packages.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual


ms.assetid: fee8d7b0-b4c2-4c70-83ff-bc285551ee68
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Operating system deployment views in Configuration Manager

The Configuration Manager operating system deployment views contain information about boot image packages, computer association state migrations, operating system image packages, task sequences, driver packages, and so on. There is also a status view that contains information about the status of task sequence steps.

The following sections provide detailed information about operating system deployment views and operating system deployment status views.

## Operating system deployment views

The operating system deployment views are described in this section.

### v_BootImagePackage

Lists the boot image packages in the Configuration Manager site hierarchy, including package ID, package name, the path of the package source files, source site, priority, package flags, last refresh time, and more.
The view can be joined to other views by using the **PackageID** column.

### v_BootImagePackage_References

Lists the boot image packages, by **pkgID**, the configuration item ID for the drivers that have been added to the boot image package, as well as the path to the driver source files.
The view can be joined to the **v_ConfigurationItems** view by using the **CI_ID** column and other views by using the **PkgID** column, which contains the same package ID information as the **PackageID** column in other views.

### v_DriverContentToPackage

Lists the driver packages, by package ID and package name, the configuration item IDs for the drivers contained in the package, and the content IDs for the drivers.
The view can be joined to the **v_ConfigurationItems** view by using the **CI_ID** column, the **v_Contents** view by using the **Content_ID** column, and other views by using the **PkgID** column, which contains the same package ID Information as the **PackageID** column in other views.

### v_DriverPackage

Lists the driver packages in the Configuration Manager site hierarchy, including package ID, package name, the path of the package source files, source site, priority, package flags, last refresh time, and more. The driver packages are created in the Driver Packages node of the Configuration Manager console.
The view can be joined to other views by using the **PackageID** column.

### v_ImagePackage

Lists the operating system image packages in the Configuration Manager site hierarchy, including package ID, package name, the path of the package source files, source site, priority, package flags, last refresh time, and more. The operating system image packages are created in the **Operating System Images** node of the Configuration Manager console.
The view can be joined to other views by using the **PackageID** column.

### V_LastPXEDeployment

Lists information about the last PXE deployment including the Mac address of the computer, the NetBIOS name and more.
The view can be joined to other views by using the **MachineID** column.

### v_MachineSettings

Lists the Configuration Manager clients, by **ResourceID**, that have operating system deployment computer settings, including the source site, locale, and the date the settings were last modified.
The view can be joined to other views by using the **ResourceID** column.

### v_StateMigration

Lists the computer associations, by **MigrationID**, that have been created in the **User State Migration** node of the Configuration Manager console. Computer associations organize the migration of user state and settings from a source computer to a destination computer. The view provides information about the migration type, source computer name, source client resource ID, last logged on user, restore computer name, restore client resource ID, and so on.
The view can be joined to other views by using the **SourceClientResourceID** and **RestoreClientResourceID** columns.

### v_TaskSequencePackage

Lists the task sequences in the Configuration Manager site hierarchy, including the task sequence package ID, package name, source site, priority, package flags, last refresh time, boot image package ID, and more. The **BootImageID** column contains the package ID for the boot image package defined in the task sequence. The task sequences are created in the **Task Sequences** node of the Configuration Manager console.
The view can be joined to other views by using the **PackageID** and **BootImageID** columns. The **BootImageID** column contains the same package ID information as the **ReferencePackageID** column in the **v_TaskSequenceReferencesInfo** view, and the same package ID information as the **PackageID** column in other views.

### v_TaskSequencePackageReferences

Lists the packages in a task sequence that reference other packages.
This view can be joined to other views by using the **PackageID** and **RefPackageID** columns.

### v_TaskSequenceReferenceDps

Lists the task sequences, by Task sequence ID, which is the task sequence package ID, the boot image package ID, server NAL path (path to distribution point), site code, task sequence source version, and task sequence hash.
The view can be joined to other views by using the **TaskSequenceID** and **PackageID** columns. The **TaskSequenceID** column in this view contains the same package ID information as the **PackageID** column in other views.

### v_TaskSequenceReferencesInfo

Lists the task sequences, by Package ID, and the reference package ID for the associated boot image, as well as the reference name, reference version, and so on.
The view can be joined to other views by using the **PackageID** and **RefPackageID** columns. The **RefPackageID** column contains the same package ID information as the **BootImageID** column in the **v_TaskSequencePackage** view, and the same package ID information as the **PackageID** column in other views.

### v_UserStateMigration

Lists the user accounts, by *Domain*\\*Username*, that will be migrated as specified for the computer associations created in the **User State Migration** node of the Configuration Manager console. The locale ID, source client resource ID, and restore client resource ID are also listed.
The view can be joined to other views by using the **SourceClientResourceID** and **RestoreClientResourceID** columns, which contain the same information as the **ResourceID** column in other views.

### v_TaskSequenceAppReferenceDps

Lists, by task sequence ID, information about the content packages that are associated with task sequences.
This view can be joined to other views by using the **PackageID** and **TaskSequenceID** columns.

### v_TaskSequenceAppReferencesInfo

Lists, by package ID, the content packages that are referenced by a task sequence that installs an application.
This view can be joined to other views by using the **PackageID** column.

## Operating system deployment status view

The operating system deployment status view contains status information for operating system deployment task sequence steps. For more information about the status views, see [Status and alert views in Configuration Manager](status-alert-views-configuration-manager.md). The status view that contains operating system deployment information is described in this section.

### v_TaskExecutionStatus

Lists the status for operating system deployment task sequence steps, as well as the advertisement ID, resource ID, action name, and so on.
The view can be joined to other views by using the **AdvertisementID** or **ResourceID** columns.

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)  
