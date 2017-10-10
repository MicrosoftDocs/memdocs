---
title: "Manage drivers - Configuration Manager"
description: "Use the Configuration Manager driver catalog to import device drivers, group drivers in packages, and distribute those packages to distribution points."
ms.custom: na
ms.date: 01/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
caps.latest.revision: 10
caps.handback.revision: 0
author: Dougebyms.author: dougebymanager: angrobe

---
# Manage drivers in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
System Center Configuration Manager provides a driver catalog that you can use to manage the Windows device drivers in your Configuration Manager environment. You can use the driver catalog to import device drivers into Configuration Manager, to group them in packages, and to distribute those packages to distribution points where you can access them when you deploy an operating system. Device drivers can be used when you install the full operating system on the destination computer and when you install Windows PE by using a boot image. Windows device drivers consist of a Setup Information File (INF) file and any additional files that are required to support the device. When an operating system is deployed, Configuration Manager obtains the hardware and platform information for the device from its INF file. Use the following to manage drivers in your Configuration Manager environment.

##  <a name="BKMK_DriverCategories"></a> Device Driver Categories  
 When you import device drivers, you can assign the device drivers to a category. Device driver categories help group similarly used device drivers together in the driver catalog. For example, you can assign all network adapter device drivers to a specific category. Then, when you create a task sequence that includes the [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) step, you can specify a specific category of device drivers. Configuration Manager then scans the hardware and selects the applicable drivers from that category to stage on the system for Windows Setup to use.  

##  <a name="BKMK_ManagingDriverPackages"></a> Driver packages  
 You can group similar device drivers in packages to help streamline operating system deployments. For example, you might decide to create a driver package for each computer manufacturer on your network. You can create a driver package while you are importing drivers into the driver catalog directly in the **Driver Packages** node. After the driver package is created, it must be distributed to distribution points from which Configuration Manager client computers can install the drivers as they are required. Consider the following:  

-   When you create a driver package, the source location of the package must point to an empty network share that is not used by another driver package, and the SMS Provider must have Read and Write permissions to that location.  

-   When you add device drivers to a driver package, Configuration Manager copies the device driver to the driver package source location. You can add only device drivers that have been imported and that are enabled in the driver catalog to a driver package.  

-   To copy a subset of the device drivers from an existing driver package, create a new driver package, add the subset of device drivers to the new package, and then distribute the new package to a distribution point.  

 Use the following sections to create and manage driver packages.  

###  <a name="CreatingDriverPackages"></a> Create a driver package  
 Use the following procedure to create a new driver package.  

> [!IMPORTANT]  
>  To create a driver package, you must have an empty network folder that is not used by another driver package. In most cases, you must create a new folder before you start this procedure.  

> [!NOTE]  
>  When you use task sequences to install drivers, create driver packages that contain less than 500 device drivers.  

 Use the following procedure to create a driver package.  

#### To create a driver package  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Driver Packages**.  

3.  On the **Home** tab, in the **Create** group, click **Create Driver Package**.  

4.  In the **Name** box, specify a descriptive name for the driver package.  

5.  In the **Comment** box, enter an optional description for the driver package. Ensure that the description provides information about the contents or the purpose of the driver package.  

6.  In the **Path** box, specify an empty source folder for the driver package. Enter the path to the source folder in Universal Naming Convention (UNC) format. Each driver package must use a unique folder.  

    > [!IMPORTANT]  
    >  The site server account must have **Read** and **Write** permissions to the specified source folder.  

 The new driver package does not contain any drivers. The next step is to add drivers to the package.  

 If the **Driver Packages** node contains several packages, you can add folders to the node to separate the packages into logical groups.  

###  <a name="BKMK_PackageActions"></a> Additional actions for driver packages  
 You can perform additional actions to manage driver packages when you select one or more driver packages from the **Driver Packages** node. These actions include the following:  

|Action|Description|  
|------------|-----------------|  
|**Create Prestage Content file**|Creates files that can be used to manually import content and its associated metadata. Use prestaged content when you have low network bandwidth between the site server and the distribution points where the driver package is stored.|  
|**Delete**|Removes the driver package from the **Driver Packages** node.|  
|**Distribute Content**|Distributes the driver package to distribution points, distribution point groups, and distribution point groups that are associated with collections.|  
|**Manage Access Accounts**|Adds, modifies, or removes access accounts for the driver package.<br /><br /> For more information about Package Access Accounts, see [Accounts used in Configuration Manager](../../core/plan-design/hierarchy/accounts.md).|  
|**Move**|Moves the driver package to another folder in the **Driver Packages** node.|  
|**Update Distribution Points**|Updates the device driver package on all the distribution points where the package is stored. This action copies only the content that has changed after the last time it was distributed.|  
|**Properties**|Opens the **Properties** dialog box where you can review and change the content and properties of the device driver. For example, you can change the name and description of the device driver, enable the device driver, and specify on which platforms the device driver can be run.|  

##  <a name="BKMK_DeviceDrivers"></a> Device drivers  
 You can install device drivers on destination computers without including them in the operating system image that is being deployed. Configuration Manager provides a driver catalog that contains references to all the device drivers that you import into Configuration Manager. The driver catalog is located in the **Software Library** workspace and consists of two nodes: **Drivers** and **Driver Packages**. The **Drivers** node lists all the drivers that you have imported into the driver catalog. Use this node to discover the details about each imported driver, modify the drivers in a  driver package or boot image, enable or disable a driver, and so on.  

###  <a name="BKMK_ImportDrivers"></a> Import device drivers into the driver catalog  
 You must import device drivers into the driver catalog before you can use them when you deploy an operating system. To better manage your device drivers, import only those device drivers that you plan to install as part of your operating system deployment. However, you can also store multiple versions of device drivers in the driver catalog to provide an easy way to upgrade existing device drivers when hardware device requirements change on your network.  

 As part of the import process for the device driver, Configuration Manager reads the provider, class, version, signature, supported hardware, and supported platform information that is associated with the device. By default, the driver is named after the first hardware device that it supports; however, you can rename the device driver later. The supported platforms list is based on the information in the INF file of the driver. Because the accuracy of this information can vary, manually verify that the device driver is supported after it is imported into the driver catalog.  

 After you import device drivers into the catalog, you can add the device drivers to driver packages or to boot image packages.  

> [!IMPORTANT]  
>  You cannot import device drivers directly into a subfolder of the **Drivers** node. To import a device driver into a subfolder, first import the device driver into the **Drivers** node, and then move the driver to the subfolder.  

 Use the following procedure to import Windows device drivers.  

#### To import Windows device drivers into the driver catalog  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Drivers**.  

3.  On the **Home** tab, in the **Create** group, click **Import Driver** to start the **Import New Driver Wizard**.  

4.  On the **Locate Driver** page, specify the following options, and then click **Next**:  

    -   **Import all drivers in the following network path (UNC)**: To import all the device drivers that are contained in a specific folder, specify the network path to the device driver folder. For example:  **\\\servername\folder**.  

        > [!NOTE]  
        >  The process to import all drivers can take some time if there are a lot of folders and a lot of driver files (.inf).  

    -   **Import a specific driver**: To import a specific driver from a folder, specify the network path (UNC) to the Windows device driver .INF or mass storage Txtsetup.oem file of the driver.  

    -   **Specify the option for duplicate drivers**: Select how you want Configuration Manager to manage driver categories when a duplicate device drive is imported.  

    > [!IMPORTANT]  
    >  When you import drivers, the site server must have **Read** permission to the folder, or the import fails.  

5.  On the **Driver Details** page, specify the following options, and then click **Next**:  

    -   **Hide drivers that are not in a storage or network class (for boot images)**: Use this setting to only display storage and network drivers, and hide other drivers that are not typically needed for boot images, such as a video driver or modem driver.  

    -   **Hide drivers that are not digitally signed**: Use this setting to hide drivers that are not digitally signed.  

    -   In the list of drivers, select the drivers that you want to import into the driver catalog.  

    -   **Enable these drivers and allow computers to install them**: Select this setting to let computers install the device drivers. By default, this check box is selected.  

        > [!IMPORTANT]  
        >  If a device driver is causing a problem or you want to suspend the installation of a device driver, you can disable the device driver by clearing the **Enable these drivers and allow computers to install them** check box. You can also disable drivers after they have been imported.  

    -   To assign the device drivers to an administrative category for filtering purposes, such as "Desktops" or "Notebooks" categories, click **Categories** and select an existing category or create a new category. You can also use the category assignment to configure which device drivers that are applied to the deployment by the [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) task sequence step.  

6.  On the **Add Driver to Packages** page, choose whether to add the drivers to a package and then click **Next**. Consider the following to add the drivers to a package:  

    -   Select the driver packages that are used to distribute the device drivers.  

         Optionally, click **New Package** to create a new driver package. When you create a new driver package, you must provide a network share that is not in use by other driver packages.  

    -   If the package has already been distributed to distribution points, click **Yes** in the dialog box to update the boot images on distribution points. You cannot use device drivers until they are distributed to distribution points. If you click **No**, you must run the **Update Distribution Point** action before the boot image will contain the updated drivers. If the driver package has never been distributed, you must click **Distribute Content** from the **Driver Packages** node.  

7.  On the **Add Driver to Boot Images** page, choose whether to add the device drivers  to existing boot images, and then click **Next**. If you select a boot image, consider the following:  

    > [!NOTE]  
    >  As a best practice, add only mass storage and network device drivers to the boot images for operating system deployment scenarios.  

    -   Click **Yes** in the dialog box to update the boot images on distribution points. You cannot use device drivers until they are distributed to distribution points. If you click **No**, you must run the **Update Distribution Point** action before the boot image will contain the updated drivers. If the driver package has never been distributed, you must click **Distribute Content** from the **Driver Packages** node.  

    -   Configuration Manager warns you if the architecture for one or more drivers does not match the architecture of the boot images that you selected. If they do not match, click **OK** and go back to the **Driver Details** page to clear the drivers that do not match the architecture of the selected boot image. For example, if you select an x64 and x86 boot image, all drivers must support both architectures. If you select an x64 boot image, all drivers must support the x64 architecture.  

        > [!NOTE]  
        >  -   The architecture is based on the architecture reported in the .INF from the manufacturer.  
        > -   If a driver reports it supports both architectures then you can import it into either boot image.  

    -   Configuration Manager warns you if you add device drivers that are not network or storage drivers to a boot image because in most cases they are not necessary for the boot image. Click **Yes** to add the drivers to the boot image or **No** to go back and modify your driver selection.  

    -   Configuration Manager warns you if one or more of the selected drivers are not properly digitally signed. Click **Yes** to continue and click **No** to go back and make changes to your driver selection.  

8.  Complete the wizard.  

###  <a name="BKMK_ModifyDriverPackage"></a> Manage device drivers in a driver package  
 Use the following procedures to modify driver packages and boot images. To add or remove device drivers, locate the drivers in the **Drivers** node, and then edit the packages or boot images that the selected drivers are associated with.  

#### To modify the device drivers in a driver package  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Drivers**.  

3.  In the **Drivers** node, select the device drivers that you want to add to the driver package.  

4.  On the **Home** tab, in the **Driver** group, click **Edit**, and then click **Driver Packages**.  

5.  To add a device driver, select the check box of the driver packages to which you want to add the device drivers. To remove a device driver, clear the check box of the driver packages from which you want to remove the device driver.  

     If you are adding device drivers that are associated with driver packages, you can optionally create a new package, by clicking **New Package**, which opens the **New Driver Package** dialog box.  

6.  If the package has already been distributed to distribution points, click **Yes** in the dialog box to update the boot images on distribution points. You cannot use device drivers until they are distributed to distribution points. If you click **No**, you must run the **Update Distribution Point** action before the boot image will contain the updated drivers. If the driver package has never been distributed, you must click **Distribute Content** from the **Driver Packages** node. Before the drivers are available, you must update the driver package on distribution points.  

     Click **OK**.  

###  <a name="BKMK_ManageDriversBootImage"></a> Manage device drivers in a boot image  
 You can add Windows device drivers that have been imported into the driver catalog to boot images. Use the following guidelines when you add device drivers to a boot image:  

-   Add only mass storage and network adapter device drivers to boot images because other types of drivers are not generally required. Drivers that are not required increase the size of the boot image unnecessarily.  

-   Add only device drivers for Windows 10 to a boot image because the required version of Windows PE is based on Windows 10.  

-   Ensure that you use the correct device driver for the architecture of the boot image.  Do not add an x86 device driver to an x64 boot image.  

 Use the following procedure to add or remove device drivers in a boot image.  

#### To modify the  device drivers associated with a boot image  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Drivers**.  

3.  In the **Drivers** node, select the device drivers that you want to add to the driver package.  

4.  On the **Home** tab, in the **Driver** group, click **Edit**, and then click **Boot images**.  

5.  To add a device driver, select the check box of the boot image to which you want to add the device drivers. To remove a device driver, clear the check box of the boot image from which you want to remove the device driver.  

6.  If you do not want to update the distribution points where the boot image is stored, clear the **Update distribution points when finished** check box. By default, the distribution points are updated when the boot image is updated.  

     Click **OK** and consider the following:  

    -   Click **Yes** in the dialog box to update the boot images on distribution points. You cannot use device drivers until they are distributed to distribution points. If you click **No**, you must run the **Update Distribution Point** action before the boot image will contain the updated drivers. If the driver package has never been distributed, you must click **Distribute Content** from the **Driver Packages** node.  

    -   Configuration Manager warns you if the architecture for one or more drivers does not match the architecture of the boot images that you selected. If they do not match, click **OK** and go back to the **Driver Details** page to clear the drivers that do not match the architecture of the selected boot image. For example, if you select an x64 and x86 boot image, all drivers must support both architectures. If you select an x64 boot image, all drivers must support the x64 architecture.  

        > [!NOTE]  
        >  -   The architecture is based on the architecture reported in the .INF from the manufacturer.  
        > -   If a driver reports it supports both architectures then you can import it into either boot image.  

    -   Configuration Manager warns you if you add device drivers that are not network or storage drivers to a boot image because in most cases they are not necessary for the boot image. Click **Yes** to add the drivers to the boot image or **No** to go back and modify your driver selection.  

    -   Configuration Manager warns you if one or more of the selected drivers are not properly digitally signed. Click **Yes** to continue and click **No** to go back and make changes to your driver selection.  

7.  Click **OK**.  

###  <a name="BKMK_DriverActions"></a> Additional actions for device drivers  
 You can perform additional actions to manage device drivers when you select one or more device drivers from the **Drivers** node. These actions include the following:  

|Action|Description|  
|------------|-----------------|  
|**Categorize**|Clears, manages, or sets an administrative category for the selected device drivers.|  
|**Delete**|Removes the device driver from the **Drivers** node and also removes the driver from the associated distribution points.|  
|**Disable**|Prohibits the device driver from being installed. You can temporarily disable device drivers so that Configuration Manager client computers and task sequences cannot install them when you are deploying operating systems. **Note:**  The Disable action only prevents drivers from installing using the Auto Apply Driver task sequence step.|  
|**Enable**|Lets Configuration Manager client computers and task sequences install the device driver when the operating system is deployed.|  
|**Move**|Moves the device driver to another folder in the **Drivers** node.|  
|**Properties**|Opens the **Properties** dialog box where you can review and change the properties of the device driver. For example, you can change the name and description of the device driver, enable the device driver, and specify which platforms the device driver can be run on.|  

##  <a name="BKMK_TSDrivers"></a> Use task sequences to install device drivers  
 Use task sequences to automate how the operating system is deployed. Each step in the task sequence can perform a specific action, such as installing a device driver. You can use the following two task sequence steps to install device drivers while you are deploying operating systems:  

-   [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers): This step lets you automatically match and install device drivers as part of an operating system deployment. You can configure the task sequence step to install only the best matched driver for each detected hardware device, or specify that the task sequence step installs all compatible drivers for each detected hardware device, and then let Windows Setup choose the best driver. In addition, you can specify a category of device drivers to limit the drivers that are available for this step.  

-   [Apply Driver Package](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage): This step lets you make all device drivers in a specific driver package available for Windows Setup. In the specified driver packages, Windows Setup searches for the device drivers that are required. When you create stand-alone media, you must use this step to install device drivers.  

 When you use these task sequence steps, you can also specify how the device drivers are installed on the computer where you deploy the operating system. For more information, see [Manage task sequences to automate tasks](../deploy-use/manage-task-sequences-to-automate-tasks.md).  

##  <a name="BKMK_InstallingDeviceDiriversTS"></a> Use task sequences to install device drivers on computers  
 Use the following procedure to install device drivers as part of the operating system deployment.  

#### Use a task sequence to install device drivers  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  In the **Task Sequences** node, select the task sequence that you want to modify to install the device driver, and then click **Edit**.  

4.  Move to the location where you want to add the **Driver** steps, click **Add**, and then select **Drivers**.  

5.  Add the **Auto Apply Drivers** step if you want the task sequence to install all the device drivers or the specific categories that are specified. Specify the options for the step on the **Properties** tab and any conditions for the step on the **Options** tab.  

     Add the **Apply Driver Package** step if you want the task sequence to install only those device drivers from the specified package. Specify the options for the step on the **Properties** tab and any conditions for the step on the **Options** tab.  

    > [!IMPORTANT]  
    >  You can select **Disable this step** on the **Options** tab to disable the step to troubleshoot the task sequence.  

6.  Click **OK** to save the task sequence.  

 For more information about creating a task sequence to install an operating system, see [Create a task sequence to install an operating system](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md).  

##  <a name="BKMK_DriverReports"></a> Driver management reports  
 You can use several reports in the **Driver Management** reports category to determine general information about the device drivers in the driver catalog. For more information about reports, see [Reporting](../../core/servers/manage/reporting.md).
