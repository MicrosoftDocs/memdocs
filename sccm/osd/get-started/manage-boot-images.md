---
title: "Manage boot images "
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, learn to manage the Windows PE boot images that you use during an operating system deployment."
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
caps.latest.revision: 23
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Manage boot images with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

A boot image in Configuration Manager is a [Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (WinPE) image that is used during an operating system deployment. Boot images are used to start a computer in WinPE. This minimal operating system contains limited components and services. Configuration Manager uses WinPE to prepare the destination computer for Windows installation. Use the following sections to manage boot images.

## <a name="BKMK_BootImageDefault"></a> Default boot images
Configuration Manager provides two default boot images: One to support x86 platforms and one to support x64 platforms. These images are stored in: \\\\*servername*>\SMS_<*sitecode*>\osd\boot\\<*x64*> or <*i386*>. The default boot images are updated or regenerated depending on the action that you take.

Consider the following behaviors for any of the actions described for default boot images:
- The source driver objects must be valid. These objects include the driver source files. If the objects are not valid, the site doesn't add the drivers to the boot images.
- Boot images that aren’t based on the default boot images, even if they use the same Windows PE version, are not modified.
- Redistribute the modified boot images to distribution points.
- Recreate any media that uses the modified boot images.
- If you do not want your customized/default boot images automatically updated, do not store them in the default location.

> [!NOTE]
> The Configuration Manager Trace Log Tool (CMTrace) is added to all boot images in the **Software Library**. When you're in Windows PE, start the tool by typing **CMTrace** from the command prompt. Starting in version 1802, when launching cmtrace.exe in Windows PE, you're no longer prompted to choose whether to make this program the default viewer for log files.

### Use updates and servicing to install the latest version of Configuration Manager
Beginning in version 1702, when you upgrade the Windows Assessment and Deployment Kit (ADK) version, and then use updates and servicing to install the latest version of Configuration Manager, the site regenerates the default boot images. This update includes the new WinPE version from the updated Windows ADK, the new version of the Configuration Manager client, drivers, and customizations. The site doesn't modify custom boot images.

Prior to version 1702, Configuration Manager updates the existing boot image with the client components, drivers, and customizations, but doesn't use the latest WinPE version from the Windows ADK. Manually modify the boot image to use the new version of the Windows ADK.

### Upgrade from Configuration Manager 2012 to Configuration Manager Current Branch (CB)
When you upgrade Configuration Manager 2012 to Configuration Manager CB by using the setup process, the site regenerates the default boot images. This update includes the new WinPE version from the updated Windows ADK and the new version of the Configuration Manager client. All boot image customizations remain unchanged. The site doesn't modify custom boot images.

### Update distribution points with the boot image
When you use the **Update Distribution Points** action from the **Boot Images** node in the console, the site updates the target boot image with the client components, drivers, and customizations.    

Beginning in Configuration Manager version 1706, reload the boot image with latest version of WinPE from the Windows ADK installation directory. The **General** page of the Update Distribution Points wizard provides the following information: 
 - The Windows ADK version installed on the site server
 - The Windows ADK version of WinPE in the boot image
 - The version of the Configuration Manager client
Use this information to help decide whether to reload the boot image. The **Boot Images** node also includes a new column for (**Client Version**). Use this column to quickly view the Configuration Manager client version in each boot image.    


##  <a name="BKMK_BootImageCustom"></a> Customize a boot image  
 When a boot image is based on the WinPE version from the supported version of the Windows ADK, you can customize or [modify a boot image](#BKMK_ModifyBootImages) from the console. When a site is upgraded with a new version and a new version of Windows ADK is installed, custom boot images (not in the default boot image location) aren't updated with the new version of Windows ADK. When that happens, you can't customize the boot images in the Configuration Manager console. However, they continue to work as they did before the upgrade.  

 When a boot image is based on a different version of the Windows ADK installed on a site, you must customize the boot images. Use another method to customize these boot images, such as using the Deployment Image Servicing and Management (DISM) command-line tool. DISM is part of the Windows ADK. For more information, see [Customize boot images](customize-boot-images.md).  

##  <a name="BKMK_AddBootImages"></a> Add a boot image  

 During site installation, Configuration Manager automatically adds boot images that are based on a WinPE version from the supported version of the Windows ADK. Depending on the version of Configuration Manager, you might be able to add boot images based on a different WinPE version from the supported version the Windows ADK. An error occurs when you try to add a boot image that contains an unsupported version of WinPE. The following list is the currently supported Windows ADK and WinPE versions: 

-   **Windows ADK version**  

     Windows ADK for Windows 10  

-   **Windows PE versions for boot images customizable from the Configuration Manager console**  

     Windows PE 10  

-   **Supported Windows PE versions for boot images not customizable from the Configuration Manager console**  

     Windows PE 3.1<sup>1</sup> and Windows PE 5  

     <sup>1</sup> You can only add a boot image to Configuration Manager when it is based on Windows PE 3.1. Upgrade the Windows AIK for Windows 7 (based on Windows PE 3.0) with the Windows AIK Supplement for Windows 7 SP1 (based on Windows PE 3.1). Download the Windows AIK Supplement for Windows 7 SP1 from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188).  

     For example, use the Configuration Manager console to customize boot images based on Windows PE 10 from the Windows ADK for Windows 10. For a boot image based on Windows PE 5, customize it from a different computer using the version of DISM from the Windows ADK for Windows 8. Then add the custom boot image to the Configuration Manager console. For more information, see [Customize boot images](customize-boot-images.md).

 Use the following procedure to manually add a boot image.  

#### To add a boot image  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Boot Images**.  

3.  On the **Home** tab, in the **Create** group, click **Add Boot Image** to start the Add Boot Image Wizard.  

4.  On the **Data Source** page, specify the following options, and then click **Next**.  

    -   In the **Path** box, specify the path to the boot image WIM file.  

         The specified path must be a valid network path in the UNC format. For example: \\\\<*servername*\\<*sharename*>\\<*bootimagename*>.wim.  

    -   Select the boot image from the **Boot Image** drop-down list. If the WIM file contains multiple boot images, select the  appropriate image.  

5.  On the **General**  page, specify the following options, and then click **Next**.  

    -   In the **Name** box, specify a unique name for the boot image.  

    -   In the **Version** box, specify a version number for the boot image.  

    -   In the **Comment** box, specify a brief description of how the boot image is used.  

6.  Complete the wizard.  

 The boot image is now listed in the **Boot Image** node of the Configuration Manager console. Before using the boot image to deploy an operating system, distribute the boot image to distribution points. 

> [!NOTE]  
>  In the **Boot Image** node of the console, the **Size (KB)** column displays the decompressed size for each boot image. When the site sends a boot image over the network, it sends a compressed copy. This copy is typically smaller than the size listed in the **Size (KB)** column.  

##  <a name="BKMK_DistributeBootImages"></a> Distribute boot images to a distribution point  
 Boot images are distributed to distribution points in the same way as you distribute other content. In most cases, you must distribute the boot image to at least one distribution point before you deploy an operating system and before you create media.   

> [!NOTE]  
> To use PXE to deploy an operating system, consider the following points before you distribute the boot image:  
> - Configure the distribution point to accept PXE requests.  
> - Distribute both an x86 and an x64 PXE-enabled boot image to at least one PXE-enabled distribution point.  
> - Configuration Manager distributes the boot images to the **RemoteInstall** folder on the PXE-enabled distribution point.  
>   
> For more information about using PXE to deploy operating systems, see [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 For the steps to distribute a boot image, see [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  

##  <a name="BKMK_ModifyBootImages"></a> Modify a boot image  
 You can add or remove device drivers to the image or edit the properties associated with the boot image. The device drivers that you add or remove can include network adapters or mass storage device drivers. Consider the following factors when you modify boot images:  

-   Import and enable the device drivers in the device driver catalog before adding them to the boot image.  

-   When you modify a boot image, the boot image does not change any of the associated packages that the boot image references.  

-   After you make changes to a boot image, **update** the boot image on the distribution points that already have it. This process makes the most current version of the boot image available to clients. For more information, see [Manage content you have distributed](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage).  

 Use the following procedure to modify a boot image.  

#### To modify the properties of a boot image  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Boot Images**.  

3.  Select the boot image that you want to modify.  

4.  On the **Home** tab, in the **Properties** group, click **Properties** to open the **Properties** dialog box for the boot image.  

5.  Set any of the following settings to change the behavior of the boot image:  

    -   On the **Images** tab, if you have changed the properties of the boot image by using an external tool, click **Reload**.  

    -   On the **Drivers** tab, add the Windows device drivers that are required to boot WinPE. Consider the following points when you add device drivers:  

        -   Select **Hide drivers that do not match the architecture of the boot image** to only display only drivers for the architecture of the boot image. The architecture is based on the architecture reported in the INF from the manufacturer.  

        -   Select **Hide drivers that are not in a storage or network class (for boot images)** to only display storage and network drivers. This option also hides other drivers that are not typically needed for boot images, such as video or modem drivers.  

        -   Select **Hide drivers that are not digitally signed** to hide drivers that don't have a valid digital signature.  

        -   As a best practice, add only network and mass storage drivers to the boot image, unless there are requirements for other drivers in WinPE.  

        -   Because WinPE already comes with many drivers built in, add only network and mass storage drivers that are not supplied by WinPE.  

        -   Make sure that the drivers that you add to the boot image match the architecture of the boot image.  

        > [!NOTE]  
        >  You must import device drivers into the drivers catalog before you add them to a boot image. For information about how to import device drivers, see [Manage drivers](manage-drivers.md).  

    -   On the **Customization** tab, select any of the following settings:  

        -   Select the **Enable Prestart Commands** check box to specify a command to run before the task sequence is run. When you enable this option, also specify the command line to run and any support files required by the command.  

            > [!WARNING]  
            >  Add **cmd /c** to the start of the command line. If you do not specify **cmd /c**, the command won't close after it runs. The deployment continues to wait for the command to finish and won't start any other configured commands or actions.  

            > [!TIP]  
            >  During task sequence media creation, the wizard writes the package ID and prestart command line, including the value for any task sequence variables, to the CreateTSMedia.log log file. This log is on the computer that runs the Configuration Manager console. Review this log file to verify the value for the task sequence variables.  

        -   Set the **Windows PE Background** settings to specify whether you want to use the default WinPE background or a custom background.  

        -   Select **Enable command support (testing only)** to open a command prompt by using the **F8** key while the boot image is deployed. This option is useful for troubleshooting while you are testing your deployment. Using this setting in a production deployment is not advised.  

        -   Configure the Windows PE scratch space, which is temporary storage (RAM drive) used by WinPE. For example, when an application is run within WinPE and needs to write temporary files, WinPE redirects the files to the scratch space in memory to simulate the presence of a hard disk. By default, WinPE allocates 32 megabytes (MB) of writeable memory.  

    -   On the **Data Source** tab, update any of the following settings:  

        -   To change the source file of the boot image, set **Image path** and **Image index**.  

        -   To create a schedule for when the site updates the boot image, select **Update distribution points on a schedule**.  

        -   If you don't want the content of this package to age out of the client cache to make room for other content, select **Persist content in client cache**.  

        -   To specify that the site only distributes changed files when it updates the boot image package on the distribution point, select **Enable binary differential replication** (BDR). This setting minimizes the network traffic between sites. BDR is especially useful when the boot image package is large and the changes are relatively small.  

        -   If you use the boot image in a PXE-enabled deployment, select **Deploy this boot image from the PXE-enabled distribution point**.  

            > [!NOTE]  
            >  For more information, see [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   On the **Data Access** tab, select any of the following settings:  

        -   Set the **Package share settings** if you want clients to install the content in this package from the network.  

        -   Set the **Package update settings** to specify how you want Configuration Manager to disconnect users from the distribution point. Configuration Manager might be unable to update the boot image when users are connected to the distribution point.  

    -   On the **Distribution Settings** tab, select any of the following settings:  

        -   In the **Distribution priority** list, specify the priority level. Configuration Manager uses this priority list when the site distributes multiple packages to the same distribution point.  

        -   If you want to enable on-demand content distribution to preferred distribution points, select **Distribute the content for this package to preferred distribution points**. When you enable this setting, if a client requests the content for the package and the content is not available on any preferred distribution points, then the management point distributes the content to all preferred distribution points.  

        -   To specify how you want the site to distribute the boot image to distribution points that are enabled for prestaged content, set the **Prestaged distribution point settings**.  

            > [!NOTE]  
            >  For more information about prestaged content, see [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  

    -   On the **Content Locations** tab, select the distribution point or distribution point group and perform any of the following actions:  

        -   Click **Redistribute** to distribute the boot image to the selected distribution point or distribution point group again.  

        -   Click **Validate** to check the integrity of the boot image package on the selected distribution point or distribution point group.  

    -   On the **Optional Components** tab, specify the components that are added to Windows PE for use with Configuration Manager. For more information about available optional components, see [WinPE: Add packages (Optional Components Reference)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

    -   On the **Security** tab, select an administrative user and change the operations that they can perform.  

6.  After you have configured the properties, click **OK**.  

##  <a name="BKMK_BootImagePXE"></a> Configure a boot image to deploy from a PXE-enabled distribution point  
 Before you  can use a boot image for a PXE operating system deployment, you must configure the boot image to deploy from a PXE-enabled distribution point.  

#### To configure a boot image to deploy from a PXE-enabled distribution point  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Boot Images**.  

3.  Select the boot image that you want to modify.  

4.  On the **Home** tab, in the **Properties** group, click **Properties** to open the **Properties** dialog box for the boot image.  

5.  On the **Data Source** tab, select **Deploy this boot image from the PXE-enabled distribution point**.  

    > [!NOTE]  
    >  For more information, see [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

6.  After you have configured the properties, click **OK**.  

##  <a name="BKMK_BootImageLanguage"></a> Configure multiple languages for boot image deployment  
 Boot images are language neutral. This functionality allows you to use one boot image to display the task sequence text in multiple languages while in WinPE. Include the appropriate language support from the boot image **Optional Components** tab. Then set the appropriate task sequence variable to indicate which language to display. The language of the deployed operating system is independent from the language in WinPE. The language that WinPE displays to the user is determined as follows:  

-   When a user runs the task sequence from an existing operating system, Configuration Manager automatically uses the language configured for the user. When the task sequence automatically runs as the result of a mandatory deployment deadline, Configuration Manager uses the language of the operating system.  

-   For operating system deployments that use PXE or media, set the language ID value in the **SMSTSLanguageFolder** variable as part of a prestart command. When the computer boots to WinPE, messages are displayed in the language that you specified in the variable. If there is an error accessing the language resource file in the specified folder, or you do not set the variable, WinPE displays messages in the default language.  

    > [!NOTE]  
    >  When the media is protected with a password, the text that prompts the user for the password is always displayed in the WinPE language.  

 Use the following procedure to set the WinPE language for PXE or media-initiated operating system deployments.  

#### To set the Windows PE language for a PXE or media-initiated operating system deployment  

1.  Verify that the appropriate task sequence resource file (tsres.dll) is in the corresponding language folder on the site server before you update the boot image. For example, the English resource file is in the following location: <*ConfigMgrInstallationFolder*>\OSD\bin\x64\00000409\tsres.dll.  

2.  As part of your prestart command, set the SMSTSLanguageFolder environment variable to the appropriate language ID. The language ID must be specified by using decimal and not hexadecimal. For example, to set the language ID to English, specify the decimal value 1033, not the hexadecimal value 00000409 of the folder name.  
