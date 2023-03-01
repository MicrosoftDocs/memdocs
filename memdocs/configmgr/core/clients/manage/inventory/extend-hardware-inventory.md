---
title: Extend hardware inventory
titleSuffix: Configuration Manager
description: Learn ways to extend hardware inventory in Configuration Manager.
ms.date: 12/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: how-to
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to extend hardware inventory in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Hardware inventory reads information from Windows PCs by using Windows Management Instrumentation (WMI). WMI is the Microsoft implementation of web-based Enterprise Management (WBEM), an industry standard for accessing management information in an enterprise. In previous versions of Configuration Manager, you extended hardware inventory by modifying the file sms_def.mof on the site server. This file contained a list of WMI classes that could be read by hardware inventory. Editing this file, you could enable and disable existing classes, and also create new classes to inventory.

The Configuration.mof file is used to define the data classes to be inventoried by hardware inventory on the client and is unchanged from Configuration Manager 2012. You can create data classes to inventory existing or custom WMI repository data classes or registry keys present on client systems.

The Configuration.mof file also defines and registers the WMI providers that access device information during hardware inventory. Registering providers defines the type of provider to be used and the classes that the provider supports.

When Configuration Manager clients request policy, the Configuration.mof is attached to the policy body. This file is then downloaded and compiled by clients. When you add, modify, or delete data classes from the Configuration.mof file, clients automatically compile these changes that are made to inventory-related data classes. No further action is necessary to inventory new or modified data classes on Configuration Manager clients. This file is located in the `Inboxes\clifiles.src\hinv\` folder of the Configuration Manager installation directory on the primary site server or central administration site (CAS) server.

In Configuration Manager current branch, you don't edit the sms_def.mof file as with earlier versions. Instead, make these changes with client settings. Configuration Manager provides the following methods to extend hardware inventory.

> [!NOTE]
> If you changed the state of classes in client settings, when you update the site, some classes may revert to a default state. For example, if you disable the `SMS_Windows8Application` or `SMS_Windows8ApplicationUserInfo` classes, they're enabled after installing a Configuration Manager update. When you customize hardware inventory classes, make sure to review their configuration before and after a site update.<!-- 12613335 -->
>
> If you've manually changed the Configuration.mof file to add custom inventory classes, these changes will be overwritten when you update the site. To keep using custom classes after you update, add them to the **Added extensions** section of the Configuration.mof file. Don't modify anything above this section. The other sections are reserved for modification by Configuration Manager. The site backs up your custom Configuration.mof in the `data\hinvarchive\` folder of the Configuration Manager installation directory on the site server.

Starting in version 2107, you can use the administration service to set custom properties on devices.<!--8939867--> You can then use the custom properties in Configuration Manager for reporting or to create collections. For more information, see [Custom properties for devices](../../../../develop/adminservice/custom-properties.md).

## Methods

### Enable or disable

Enable or disable some of all attributes of a class that already exists on the client. This action instructs the hardware inventory agent to collect it on clients. You can do this action in default client settings, or custom device client settings. For more information, see [Enable or disable existing classes](#enable-or-disable-existing-classes).

### Add

If a WMI class exists on the client and is known to the site, this action includes it to the possible set of hardware inventory classes. You can add a new inventory class from the WMI namespace of another device. This action is only on default client settings. For more information, see [Add a new class](#add-a-new-class).

### Extend

Add a new WMI class to the client. To manually extend hardware inventory, edit the configuration.mof on the top-level site.<!-- SCCMDocs#1073 -->

If the WMI class doesn't already exist on the client, you need to extend the WMI schema:

1. Edit the configuration.mof on the top-level site. Review **dataldr.log** to see the site add it.

1. Refresh policy on a client, and wait for the new class to compile.

1. Use default client settings to [Add](#add) the new class to hardware inventory. You don't have to enable this class in default client settings. You can then enable it in a custom device client setting.

### Import and export

Use the Configuration Manager console to import and export Managed Object Format (MOF) files that contain inventory classes. For more information, see [How to import classes](#how-to-import-classes) and [How to export classes](#how-to-export-classes).

### About NOIDMIF files

Use NOIDMIF files to collect information about client devices that Configuration Manager can't inventory. For example, collect device asset number information that exists only as a label on the device. NOIDMIF inventory is automatically associated with the client device that it was collected from. For more information, see [Create NOIDMIF files](#create-noidmif-files).

### About IDMIF files

Use IDMIF files to collect information about assets in your organization that aren't associated with a Configuration Manager client. For example, projectors, photocopiers, and network printers. For more information, see [Create IDMIF files](#create-idmif-files).

## Procedures

These procedures help you to configure the default client settings for hardware inventory and they apply to all the clients in your hierarchy. If you want these settings to apply to only some clients, create a custom client device setting and assign it to a collection of specific clients. For more information, see [How to configure client settings](../../deploy/configure-client-settings.md).

### Enable or disable existing classes

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Client Settings** node.

1. Select the **Default Client Settings**. On the **Home** tab, in the **Properties** group, choose **Properties**.

1. In the **Default Client Settings** dialog box, choose **Hardware Inventory**.

1. In the **Device Settings** list, select **Set Classes**.

1. In the **Hardware Inventory Classes** dialog box, select or clear the classes and class properties to be collected by hardware inventory. You can expand classes to select or clear individual properties within that class. Use the **Search for inventory classes** field to search for individual classes.

> [!IMPORTANT]
> When you add new classes to Configuration Manager hardware inventory, the size of the inventory file that is collected and sent to the site server will increase. This might negatively affect the performance of your network and Configuration Manager site. Enable only the inventory classes that you want to collect.

### Add a new class

You can only add inventory classes from the hierarchy's top-level server by modifying the default client settings. This option isn't available when you create custom device settings.

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Client Settings** node.

1. Select the **Default Client Settings**. On the **Home** tab, in the **Properties** group, choose **Properties**.

1. In the **Default Client Settings** dialog box, choose **Hardware Inventory**.

1. In the **Device Settings** list, choose **Set Classes**.

1. In the **Hardware Inventory Classes** dialog box, choose **Add**.

1. In the **Add Hardware Inventory Class** dialog box, select **Connect**.

1. In the **Connect to Windows Management Instrumentation (WMI)** dialog box, specify the name of the computer from which you'll get the WMI classes and the WMI namespace to use to get the classes. If you want to get all classes below the specified WMI namespace, select **Recursive**. If the computer you're connecting to isn't the local computer, supply credentials for an account that has permission to access WMI on the remote computer.

1. Choose **Connect**.

1. In the **Add Hardware Inventory Class** dialog box, in the **Inventory classes** list, select the WMI classes that you want to add to Configuration Manager hardware inventory.

1. If you want to edit information about the selected WMI class, choose **Edit**, and in the **Class qualifiers** dialog box, provide the following information:

    - **Display name**: This name will be displayed in Resource Explorer.

    - **Properties**: Specify the units in which each property of the WMI class will be displayed.

      You can also set properties as a key property to help uniquely identify each instance of the class. If no key is defined for the class, and multiple instances of the class are reported from the client, only the latest instance that's found is stored in the database.

      When you've finished configuring the properties, select **OK** to close the **Class qualifiers** dialog box and the other open dialogs.

### How to import classes

You can only import inventory classes when you modify the default client settings. However, you can use custom client settings to import information that doesn't include a schema change, such as changing the property of an existing class from **True** to **False**.

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Client Settings** node.

1. Select the **Default Client Settings**. On the **Home** tab, in the **Properties** group, choose **Properties**.

1. In the **Default Client Settings** dialog box, choose **Hardware Inventory**.

1. In the **Device Settings** list, choose **Set Classes**.

1. In the **Hardware Inventory Classes** dialog box, choose **Import**.

1. In the **Import** dialog box, select the Managed Object Format (MOF) file that you want to import, and then choose **OK**. Review the items that will be imported, and then select **Import**.

### How to export classes

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Client Settings** node.

1. Select the **Default Client Settings**. On the **Home** tab, in the **Properties** group, choose **Properties**.

1. In the **Default Client Settings** dialog box, choose **Hardware Inventory**.

1. In the **Device Settings** list, choose **Set Classes**.

1. In the **Hardware Inventory Classes** dialog box, choose **Export**.

    > [!NOTE]
    > When you export classes, all currently selected classes will be exported.

1. In the **Export** dialog box, specify the Managed Object Format (MOF) file that you want to export the classes to, and then choose **Save**.

### Collect strings larger than 255 characters

You can specify the length of strings to be greater than 255 characters for hardware inventory properties. This action applies only to newly added classes and for hardware inventory properties that aren't keys.<!-- 1357389 -->

1. In the **Administration** workspace, select **Client Settings**. Choose a client device setting to edit, then select **Properties**.

1. Select **Hardware Inventory**, then **Set Classes**, and **Add**.

1. Select **Connect**.

1. Fill in **Computer Name**, **WMI namespace**, select **recursive** if needed. Provide credentials if necessary to connect. Select **Connect** to view the namespace classes.

1. Select a new class, then select **Edit**.

1. Change the **Length** of your property that's a string, other than the key, to be greater than 255. Select **OK**.

1. Make sure that the edited property is selected for **Add Hardware Inventory Class**, and select **OK**.

## Use MIF files

Use Management Information Format (MIF) files to extend hardware inventory information collected from clients by Configuration Manager. During hardware inventory, the information stored in MIF files is added to the client inventory report and stored in the site database, where you can use the data in the same ways that you use default client inventory data. There are two types of MIF files: NOIDMIF and IDMIF.

> [!IMPORTANT]
> Before you can add information from MIF files to the Configuration Manager database, create or import the class. For more information, see [Add a new class](#add-a-new-class) or [How to import classes](#how-to-import-classes) in this article.

### Create NOIDMIF files

NOIDMIF files can be used to add information to a client hardware inventory that can't normally be collected by Configuration Manager and is associated with a particular client device. For example, many companies label each computer in the organization with an asset number and then catalog these numbers manually. When you create a NOIDMIF file, this information can be added to the Configuration Manager database and be used for queries and reporting.

For more information about creating NOIDMIF files, see [About inventory](../../../../develop/core/clients/inventory/about-configuration-manager-inventory.md#about-noidmif-and-idmif-files) in the Configuration Manager SDK documentation.

> [!IMPORTANT]
> When you create a NOIDMIF file, save it in an ANSI-encoded format. If you save NOIDMIF files in UTF-8 encoded format, Configuration Manager can't read it.

After you create a NOIDMIF file, store it in the `%Windir%\CCM\Inventory\noidmifs` folder on each client. Configuration Manager collects information from NODMIF files in this folder during the next scheduled hardware inventory cycle.

### Create IDMIF files

IDMIF files can be used to add information about assets that couldn't normally be inventoried by Configuration Manager and isn't associated with a particular client device, to the Configuration Manager database. For example, you could use IDMIFS to collect information about projectors, DVD players, photocopiers, or other equipment that doesn't have a Configuration Manager client.

For more information about creating IDMIF files, see [About inventory](../../../../develop/core/clients/inventory/about-configuration-manager-inventory.md#about-noidmif-and-idmif-files) in the Configuration Manager SDK documentation.

After you create an IDMIF file, store it in the `%Windir%\CCM\Inventory\idmifs` folder on client computers. Configuration Manager collects information from this file during the next scheduled hardware inventory cycle. Declare new classes for information contained in the file by adding or importing them.

> [!NOTE]
> MIF files could contain large amounts of data and collecting this data could negatively affect the performance of your site. Enable MIF collection only when required. Configure the option **Maximum custom MIF file size (KB)** in the hardware inventory settings. For more information, see [Introduction to hardware inventory](introduction-to-hardware-inventory.md).
