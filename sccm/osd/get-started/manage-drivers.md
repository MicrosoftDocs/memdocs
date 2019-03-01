---
title: Manage drivers
titleSuffix: Configuration Manager
description: Use the Configuration Manager driver catalog to import device drivers, group drivers in packages, and distribute those packages to distribution points.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Manage drivers in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager provides a driver catalog that you can use to manage the Windows device drivers in your Configuration Manager environment. Use the driver catalog to import device drivers into Configuration Manager, to group them in packages, and to distribute those packages to distribution points where you can access them when you deploy an OS. Device drivers can be used when you install the full IS on the destination computer and when you use Windows PE in a boot image. Windows device drivers consist of a setup information (INF) file and any additional files that are required to support the device. When you deploy an OS, Configuration Manager obtains the hardware and platform information for the device from its INF file. 



## <a name="BKMK_DriverCategories"></a> Device driver categories

When you import device drivers, you can assign the device drivers to a category. Device driver categories help group similarly used device drivers together in the driver catalog. For example, you can assign all network adapter device drivers to a specific category. Then, when you create a task sequence that includes the [Auto Apply Drivers](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers) step, you can specify a category of device drivers. Configuration Manager then scans the hardware and selects the applicable drivers from that category to stage on the system for Windows Setup to use.  



## <a name="BKMK_ManagingDriverPackages"></a> Driver packages

Group similar device drivers in packages to help streamline OS deployments. For example, create a driver package for each computer manufacturer on your network. You can create a driver package when importing drivers into the driver catalog directly in the **Driver Packages** node. After you create a driver package, distribute it to distribution points. Then Configuration Manager client computers can install the drivers as required. 

Consider the following points:  

- When you create a driver package, the source location of the package must point to an empty network share that's not used by another driver package. The SMS Provider must have **Full control** permissions to that location.  

- When you add device drivers to a driver package, Configuration Manager copies it to the package source location. You can add to a driver package only device drivers that you've imported and that are enabled in the driver catalog.  

- You can copy a subset of the device drivers from an existing driver package. First, create a new driver package. Then add the subset of device drivers to the new package, and then distribute the new package to a distribution point.  

- When you use task sequences to install drivers, create driver packages that contain less than 500 device drivers.


### <a name="BKMK_CreatingDriverPackages"></a> Create a driver package  

> [!IMPORTANT]  
> To create a driver package, you must have an empty network folder that's not used by another driver package. In most cases, create a new folder before you start this procedure.  

1. In the Configuration Manager console, go to the **Software Library** workspace. Expand **Operating Systems**, and then select the **Driver Packages** node.  

2. On the **Home** tab of the ribbon, in the **Create** group, select **Create Driver Package**.  

3. Specify a descriptive **Name** for the driver package.  

4. Enter an optional **Comment** for the driver package. Use this description to provide information about the contents or the purpose of the driver package.  

5. In the **Path** box, specify an empty source folder for the driver package. Each driver package must use a unique folder. This path is required as a network location.  

   > [!IMPORTANT]  
   > The site server account must have **Full control** permissions to the specified source folder.  

The new driver package doesn't contain any drivers. The next step adds drivers to the package.  

If the **Driver Packages** node contains several packages, you can add folders to the node to separate the packages into logical groups.  


### <a name="BKMK_PackageActions"></a> Additional actions for driver packages  

You can perform additional actions to manage driver packages when you select one or more driver packages from the **Driver Packages** node. 


#### Create Prestage Content file
Creates files that you can use to manually import content and its associated metadata. Use prestaged content when you have low network bandwidth between the site server and the distribution points where the driver package is stored.

#### Delete
Removes the driver package from the **Driver Packages** node.

#### Distribute Content
Distributes the driver package to distribution points, distribution point groups, and distribution point groups that are associated with collections.

#### Manage Access Accounts
Adds, modifies, or removes access accounts for the driver package.

For more information about package access accounts, see [Accounts used in Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).

#### Move
Moves the driver package to another folder in the **Driver Packages** node.

#### Update Distribution Points
Updates the device driver package on all the distribution points where the package is stored. This action copies only the content that has changed after the last time it was distributed.

#### Properties
Opens the **Properties** dialog box where you can review and change the content and properties of the device driver. For example, you can change the name and description of the device driver, enable the device driver, and specify on which platforms the device driver can be run. 



## <a name="BKMK_DeviceDrivers"></a> Device drivers

You can install device drivers on destination computers without including them in the OS image that is deployed. Configuration Manager provides a driver catalog that contains references to all the device drivers that you import into Configuration Manager. The driver catalog is located in the **Software Library** workspace and consists of two nodes: **Drivers** and **Driver Packages**. The **Drivers** node lists all the drivers that you have imported into the driver catalog.  


### <a name="BKMK_ImportDrivers"></a> Import device drivers into the driver catalog  

You must import device drivers into the driver catalog before you can use them when you deploy an OS. To better manage your device drivers, import only the drivers that you plan to install as part of your OS deployments. Store multiple versions of drivers in the catalog to provide an easy way to upgrade existing drivers when hardware device requirements change on your network.  

As part of the import process for the device driver, Configuration Manager reads the following properties about the driver:
- Provider
- Class
- Version
- Signature
- Supported hardware
- Supported platform information

By default, the driver is named after the first hardware device that it supports. You can rename the device driver later. The supported platforms list is based on the information in the INF file of the driver. Because the accuracy of this information can vary, manually verify that the driver is supported after you import it into the catalog.  

After you import device drivers into the catalog, add them to driver packages or boot image packages.  

> [!IMPORTANT]  
> You can't import device drivers directly into a subfolder of the **Drivers** node. To import a device driver into a subfolder, first import the device driver into the **Drivers** node, and then move the driver to the subfolder.  


#### Process to import Windows device drivers into the driver catalog  

1. In the Configuration Manager console, go to the **Software Library** workspace. Expand **Operating Systems**, and select the **Drivers** node.  

2. On the **Home** tab of the ribbon, in the **Create** group, select **Import Driver** to start the **Import New Driver Wizard**.  

3. On the **Locate Driver** page, specify the following options:  

    - **Import all drivers in the following network path (UNC)**: To import all the device drivers in a specific folder, specify its network path. For example: `\\servername\share\folder`.  

        > [!NOTE]  
        > If there are a lot of subfolders and a lot of driver INF files, this process can take time.  

    - **Import a specific driver**: To import a specific driver from a folder, specify the network path to the Windows device driver INF file.  

    - **Specify the option for duplicate drivers**: Select how you want Configuration Manager to manage driver categories when you import a duplicate device driver  
        - **Import the driver and append a new category to the existing categories**  
        - **Import the driver and keep the existing categories**  
        - **Import the driver and overwrite the existing categories**  
        - **Do not import the driver**  

    > [!IMPORTANT]  
    > When you import drivers, the site server must have **Read** permission to the folder, or the import fails.  

4. On the **Driver Details** page, specify the following options:  

    - **Hide drivers that are not in a storage or network class (for boot images)**: Use this setting to only display storage and network drivers. This option hides other drivers that aren't typically needed for boot images, such as a video driver or modem driver.  

    - **Hide drivers that are not digitally signed**: Microsoft recommends only using drivers that are digitally signed  

    - In the list of drivers, select the drivers that you want to import into the driver catalog.  

    - **Enable these drivers and allow computers to install them**: Select this setting to let computers install the device drivers. This option is enabled by default.  

        > [!IMPORTANT]  
        > If a device driver is causing a problem or you want to suspend the installation of a device driver, disable it during import. You can also disable drivers after you import them.  

    - To assign the device drivers to an administrative category for filtering purposes, such as "Desktops" or "Notebooks", select **Categories**. Then choose an existing category, or create a new category. Use categories to control which device drivers are applied by the [Auto Apply Drivers](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers) task sequence step.  

5. On the **Add Driver to Packages** page, choose whether to add the drivers to a package.  

    - Select the driver packages that are used to distribute the device drivers.  

        If necessary, select **New Package** to create a new driver package. When you create a new driver package, provide a network share that's not in use by other driver packages.  

    - If the package has already been distributed to distribution points, select **Yes** in the dialog box to update the boot images on distribution points. You can't use device drivers until they are distributed to distribution points. If you select **No**, run the **Update Distribution Point** action before using the boot image. If the driver package has never been distributed, you must use the **Distribute Content** action in the **Driver Packages** node.  

6. On the **Add Driver to Boot Images** page, choose whether to add the device drivers to existing boot images.  

    > [!NOTE]  
    > Add only storage and network drivers to the boot images.  

    - Select **Yes** in the dialog box to update the boot images on distribution points. You can't use device drivers until they are distributed to distribution points. If you select **No**, run the **Update Distribution Point** action before using the boot image. If the driver package has never been distributed, you must use the **Distribute Content** action in the **Driver Packages** node.  

    - Configuration Manager warns you if the architecture for one or more drivers doesn't match the architecture of the boot images that you selected. If they don't match, select **OK**. Go back to the **Driver Details** page, and clear the drivers that don't match the architecture of the selected boot image. For example, if you select an x64 and x86 boot image, all drivers must support both architectures. If you select an x64 boot image, all drivers must support the x64 architecture.  

        > [!NOTE]  
        > - The architecture is based on the architecture reported in the INF from the manufacturer.  
        > - If a driver reports it supports both architectures, then you can import it into either boot image.  

    - Configuration Manager warns you if you add device drivers that aren't network or storage drivers to a boot image. In most cases they aren't necessary for the boot image. Select **Yes** to add the drivers to the boot image, or **No** to go back and modify your driver selection.  

    - Configuration Manager warns you if one or more of the selected drivers aren't properly digitally signed. Select **Yes** to continue, and select **No** to go back and make changes to your driver selection.  

7. Complete the wizard.  


### <a name="BKMK_ModifyDriverPackage"></a> Manage device drivers in a driver package  

Use the following procedures to modify driver packages and boot images. To add or remove device drivers, locate the drivers in the **Drivers** node, and then edit the packages or boot images with which the selected drivers are associated.  

1. In the Configuration Manager console, go to the **Software Library** workspace. Expand **Operating Systems**, and then select the **Drivers** node.  

2. Select the device drivers that you want to add to a driver package.  

3. On the **Home** tab of the ribbon, in the **Driver** group, select **Edit**, and then choose **Driver Packages**.  

4. To add a device driver, select the check box of the driver packages to which you want to add the device drivers. To remove a device driver, clear the check box of the driver packages from which you want to remove the device driver.  

        If you're adding device drivers that are associated with driver packages, you can optionally create a new package. Select **New Package**, which opens the **New Driver Package** dialog box.  

5. If the package has already been distributed to distribution points, select **Yes** in the dialog box to update the boot images on distribution points. You can't use device drivers until they are distributed to distribution points. If you select **No**, run the **Update Distribution Point** action before using the boot image. If the driver package has never been distributed, you must use the **Distribute Content** action in the **Driver Packages** node. Before the drivers are available, you must update the driver package on distribution points.  

        Select **OK** when finished.  


### <a name="BKMK_ManageDriversBootImage"></a> Manage device drivers in a boot image  

You can add to boot images Windows device drivers that have been imported into the catalog. Use the following guidelines when you add device drivers to a boot image:  

- Add only storage and network drivers to boot images. Other types of drivers aren't generally required in Windows PE. Drivers that aren't required unnecessarily increase the size of the boot image.  

- Add only device drivers for Windows 10 to a boot image. The required version of Windows PE is based on Windows 10.  

- Make sure that you use the correct device driver for the architecture of the boot image. Don't add an x86 device driver to an x64 boot image.  

#### Process to modify the device drivers associated with a boot image  

1. In the Configuration Manager console, go to the **Software Library** workspace. Expand **Operating Systems**, and then select the **Drivers** node.  

2. Select the device drivers that you want to add to the driver package.  

3. On the **Home** tab of the ribbon, in the **Driver** group, select **Edit**, and then choose **Boot images**.  

4. To add a device driver, select the check box of the boot image to which you want to add the device drivers. To remove a device driver, clear the check box of the boot image from which you want to remove the device driver.  

5. If you don't want to update the distribution points where the boot image is stored, clear the **Update distribution points when finished** check box. By default, the distribution points are updated when the boot image is updated.  

    - Select **Yes** in the dialog box to update the boot images on distribution points. You can't use device drivers until they're distributed to distribution points. If you select **No**, run the **Update Distribution Point** action before using the boot image. If the driver package has never been distributed, you must use the **Distribute Content** action in the **Driver Packages** node.  

    - Configuration Manager warns you if the architecture for one or more drivers doesn't match the architecture of the boot images that you selected. If they don't match, select **OK**. Go back to the **Driver Details** page and clear the drivers that don't match the architecture of the selected boot image. For example, if you select an x64 and x86 boot image, all drivers must support both architectures. If you select an x64 boot image, all drivers must support the x64 architecture.  

        > [!NOTE]
        > - The architecture is based on the architecture reported in the INF from the manufacturer.  
        > - If a driver reports it supports both architectures then you can import it into either boot image.  

    - Configuration Manager warns you if you add device drivers that aren't network or storage drivers to a boot image. In most cases, they aren't necessary for the boot image. Select **Yes** to add the drivers to the boot image or **No** to go back and modify your driver selection.  

    - Configuration Manager warns you if one or more of the selected drivers aren't properly digitally signed. Select **Yes** to continue or select **No** to go back and make changes to your driver selection.  


### <a name="BKMK_DriverActions"></a> Additional actions for device drivers  

You can perform additional actions to manage device drivers when you select one or more device drivers from the **Drivers** node.  

#### Categorize
Clears, manages, or sets an administrative category for the selected device drivers.

#### Delete
Removes the device driver from the **Drivers** node and also removes the driver from the associated distribution points.

#### Disable
Prohibits the device driver from being installed. You can temporarily disable device drivers so that Configuration Manager client computers and task sequences can't install them when you're deploying operating systems. 

> [!Note]  
> This action only prevents drivers from installing using the **Auto Apply Driver** task sequence step.

#### Enable
Lets Configuration Manager client computers and task sequences install the device driver when you deploy the OS.

#### Move
Moves the device driver to another folder in the **Drivers** node.

#### Properties
Opens the **Properties** dialog box where you can review and change the properties of the device driver. For example, you can change the name and description of the device driver, enable the device driver, and specify which platforms the device driver can be run on.



## <a name="BKMK_TSDrivers"></a> Use task sequences to install device drivers  

Use task sequences to automate how the OS is deployed. Each step in the task sequence can perform a specific action, such as installing a device driver. You can use the following two task sequence steps to install device drivers while you are deploying operating systems:  

- [Auto Apply Drivers](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers): This step lets you automatically match and install device drivers as part of an operating system deployment. You can configure the task sequence step to install only the best matched driver for each detected hardware device, or specify that the task sequence step installs all compatible drivers for each detected hardware device, and then let Windows Setup choose the best driver. In addition, you can specify a category of device drivers to limit the drivers that are available for this step.  

- [Apply Driver Package](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage): This step lets you make all device drivers in a specific driver package available for Windows Setup. In the specified driver packages, Windows Setup searches for the device drivers that are required. When you create stand-alone media, you must use this step to install device drivers.  

When you use these task sequence steps, you can also specify how the device drivers are installed on the computer where you deploy the OS. For more information, see [Manage task sequences to automate tasks](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks).  



## <a name="BKMK_DriverReports"></a> Driver management reports  

You can use several reports in the **Driver Management** reports category to determine general information about the device drivers in the driver catalog. For more information about reports, see [Reporting](/sccm/core/servers/manage/reporting).

