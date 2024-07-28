---
title: Manage boot images
titleSuffix: Configuration Manager
description: In Configuration Manager, learn to manage the Windows PE boot images that you use during an OS deployment.
ms.date: 12/01/2021
ms.service: configuration-manager
ms.subservice: osd
ms.topic: how-to
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Manage boot images with Configuration Manager

*Applies to: Configuration Manager (current branch)*

A boot image in Configuration Manager is a [Windows PE](/windows-hardware/manufacture/desktop/winpe-intro) (WinPE) image that's used during an OS deployment. Boot images are used to start a computer in WinPE. This minimal OS contains limited components and services. Configuration Manager uses WinPE to prepare the destination computer for Windows installation.

## Default boot images

Configuration Manager provides two default boot images: One to support x86 platforms and one to support x64 platforms. These images are stored in the *x64* or *i386* folders in the following share on the site server: `\\<SiteServerName>\SMS_<sitecode>\osd\boot\`. The default boot images are updated or regenerated depending on the action that you take.

Consider the following behaviors for any of the actions described for default boot images:

- The source driver objects must be valid. These objects include the driver source files. If the objects aren't valid, the site doesn't add the drivers to the boot images.  

- Boot images that aren't based on the default boot images, even if they use the same Windows PE version, aren't modified.  

- Redistribute the modified boot images to distribution points.  

- Recreate any media that uses the modified boot images.  

- If you don't want your customized/default boot images automatically updated, don't store them in the default location.  

> [!NOTE]
> The Configuration Manager log tool (**CMTrace**) is added to all boot images in the **Software Library**. When you're in Windows PE, start the tool by typing `cmtrace` from the command prompt.
>
> CMTrace is the default viewer for log files in Windows PE.

### Use updates and servicing to install the latest version of Configuration Manager

When you upgrade the Windows Assessment and Deployment Kit (ADK) version, and then use updates and servicing to install the latest version of Configuration Manager, the site regenerates the default boot images. This update includes the new WinPE version from the updated Windows ADK, the new version of the Configuration Manager client, drivers, and customizations. The site doesn't modify custom boot images.

> [!NOTE]
> The site always uses the production version of the Configuration Manager client in default boot images. Even if you configure automatic client upgrades to use a [pre-production collection](../../core/clients/manage/upgrade/test-client-upgrades.md), that feature doesn't apply to boot images.<!-- 9616354 -->

### Upgrade from Configuration Manager 2012 to current branch

When you upgrade Configuration Manager 2012 to current branch, the site regenerates the default boot images. This update includes the new WinPE version from the updated Windows ADK and the new version of the Configuration Manager client. All boot image customizations remain unchanged. The site doesn't modify custom boot images.

### Update distribution points with the boot image

When you use the **Update Distribution Points** action from the **Boot Images** node in the console, the site updates the target boot image with the client components, drivers, and customizations.

You can reload the boot image with the latest version of WinPE from the Windows ADK installation directory. The **General** page of the Update Distribution Points wizard provides the following information:

- The current Windows ADK version installed on the site server
- The current production client version
- The Windows ADK version of WinPE in the boot image
- The version of the Configuration Manager client in the boot image

If the versions in the boot image are out of date, use the option to **Reload this boot image with the current Windows PE version from the Windows ADK**.

> [!IMPORTANT]
> This action is available for both default and custom boot images. During this process to reload the boot image, the site doesn't retain any manual customizations made outside of Configuration Manager. These customizations include third-party extensions. This option rebuilds the boot image using the latest version of WinPE and the latest client version. Only the configurations that you specify on the properties of the boot image are reapplied. <!--SCCMDocs issue #1283-->

The **Boot Images** node also includes a new column for (**Client Version**). Use this column to quickly view the Configuration Manager client version in each boot image.

After you update the Windows ADK on the site server, the console won't immediately show the new version. If you use one these actions to update a boot image, the site uses the latest ADK version. To get the console to display the current ADK version, restart the WMI service. For more information, see [Starting and Stopping the WMI Service](/windows/win32/wmisdk/starting-and-stopping-the-wmi-service).<!-- 2839864 -->

## Customize a boot image  

When a boot image is based on the WinPE version from the supported version of the Windows ADK, you can customize or [modify a boot image](#modify-a-boot-image) from the console. When you upgrade a site and install a new version of the Windows ADK, custom boot images aren't updated with the new version of Windows ADK. When that happens, you can't customize the boot images in the Configuration Manager console. However, they continue to work as they did before the upgrade.  

When a boot image is based on a different version of the Windows ADK installed on a site, you must customize the boot images. Use another method to customize these boot images, such as using the Deployment Image Servicing and Management (DISM) command-line tool. DISM is part of the Windows ADK. For more information, see [Customize boot images](customize-boot-images.md).  

## Add a boot image

During site installation, Configuration Manager automatically adds boot images that are based on a WinPE version from the [supported version of the Windows ADK](../../core/plan-design/configs/support-for-windows-adk.md). Depending on the version of Configuration Manager, you can add boot images based on a different WinPE version from the supported version the Windows ADK. An error occurs when you try to add a boot image that contains an unsupported version of WinPE.

Configuration Manager also supports Windows PE versions for boot images that aren't customizable from the Configuration Manager console. For example, you install the Windows ADK and WinPE add-on for Windows 11 on the site server. For x64 boot images based on WinPE version 11 from the WinPE add-on for Windows 11, you can customize them from the Configuration Manager console. However, while x86 boot images based on WinPE version 10 are supported, you need to manually customize them from a different computer. Use the version of DISM that's installed with the Windows ADK for Windows 10. Then, you can add the boot image to the Configuration Manager console.

For more information, see the following articles:

- [Customize boot images](customize-boot-images.md)
- [Support for the Windows ADK](../../core/plan-design/configs/support-for-windows-adk.md)
- [DISM supported platforms](/windows-hardware/manufacture/desktop/dism-supported-platforms)

Use the following process to add a boot image in Configuration Manager:

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Boot Images** node.  

2. On the **Home** tab of the ribbon, in the **Create** group, select **Add Boot Image**. This action starts the Add Boot Image Wizard.  

3. On the **Data Source** page, specify the following options:  

    - In the **Path** box, specify the path to the boot image WIM file. The specified path must be a valid network path in the UNC format. For example: `\\ServerName\ShareName\BootImageName.wim`

    - Select the boot image from the **Boot Image** drop-down list. If the WIM file contains multiple boot images, select the appropriate image.  

4. On the **General** page, specify the following options:  

    - In the **Name** box, specify a unique name for the boot image.  

    - In the **Version** box, specify a version number for the boot image.  

    - In the **Comment** box, specify a brief description of how you use the boot image.  

5. Complete the wizard.  

The boot image is now listed in the **Boot Image** node. Before using the boot image to deploy an OS, distribute the boot image to distribution points.

> [!TIP]
> In the **Boot Image** node of the console, the **Size (KB)** column displays the decompressed size for each boot image. When the site sends a boot image over the network, it sends a compressed copy. This copy is typically smaller than the size listed in the **Size (KB)** column.  

## Distribute boot images

Boot images are distributed to distribution points in the same way as you distribute other content. Before you deploy an OS or create media, distribute the boot image to at least one distribution point.

For more information on how to distribute a boot image, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

To use PXE to deploy an OS, consider the following points before you distribute the boot image:  

- Configure the distribution point to accept PXE requests.  
- Distribute both an x86 and an x64 PXE-enabled boot image to at least one PXE-enabled distribution point.  
- Configuration Manager distributes the boot images to the **RemoteInstall** folder on the PXE-enabled distribution point.  
  
For more information about using PXE to deploy operating systems, see [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## Modify a boot image

Add or remove device drivers to the image, or edit the properties of the boot image. The drivers that you add or remove can include network or storage drivers. Consider the following factors when you modify boot images:  

- Before adding drivers to the boot image, import and enable them in the device driver catalog.  

- When you modify a boot image, the boot image doesn't change any of the associated packages that the boot image references.  

- After you make changes to a boot image, **update** the boot image on the distribution points that already have it. This process makes the most current version of the boot image available to clients. For more information, see [Manage content you've distributed](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### Modify the properties of a boot image

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Boot Images** node.  

2. Select the boot image that you want to modify.  

3. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.  

4. Set any of the following settings to change the behavior of the boot image:  

#### Images

On the **Images** tab, if you change the properties of the boot image by using an external tool, select **Reload**.  

#### Drivers

On the **Drivers** tab, add the Windows device drivers that WinPE requires to boot. Consider the following points when you add device drivers:  

- Make sure that the drivers that you add to the boot image match the architecture of the boot image.  

- To only display drivers for the architecture of the boot image, select **Hide drivers that do not match the architecture of the boot image**. The architecture of the driver is based on the architecture reported in the INF from the manufacturer.  

- WinPE already comes with many drivers built-in. Add only network and storage drivers that aren't included in WinPE.  

- Add only network and storage drivers to the boot image, unless there are requirements for other drivers in WinPE.  

- To only display storage and network drivers, select **Hide drivers that are not in a storage or network class (for boot images)**. This option also hides other drivers that aren't typically needed for boot images, such as video or modem drivers.  

- To hide drivers that don't have a valid digital signature, select **Hide drivers that are not digitally signed**.  

> [!NOTE]  
> Import device drivers into the drivers catalog before you add them to a boot image. For information about how to import device drivers, see [Manage drivers](manage-drivers.md).  

#### Customization

On the **Customization** tab, select any of the following settings:  

- Select the **Enable Prestart Commands** option to specify a command to run before the task sequence runs. When you enable this option, also specify the command line to run and any support files required by the command.  

    > [!WARNING]  
    > Add `cmd /c` to the start of the command line. If you don't specify `cmd /c`, the command won't close after it runs. The deployment continues to wait for the command to finish and won't start any other configured commands or actions.  

    > [!TIP]  
    > During task sequence media creation, the wizard writes the package ID and prestart command line to the **CreateTSMedia.log** file. This information includes the value for any task sequence variables. This log is on the computer that runs the Configuration Manager console. Review this log file to verify the values for the task sequence variables.  

- Set the **Windows PE Background** settings to specify whether you want to use the default WinPE background or a custom background.  

- Configure the **Windows PE scratch space (MB)**, which is temporary storage (RAM drive) used by WinPE. For example, when an application is run within WinPE and needs to write temporary files, WinPE redirects the files to the scratch space in memory to simulate the presence of a hard disk. By default, this amount is 512 MB for devices with more than 1 GB of RAM, otherwise the default is 32 MB.  

- Select **Enable command support (testing only)** to open a command prompt by using the **F8** key while the boot image is deployed. This option is useful for troubleshooting while you're testing your deployment. Using this setting in a production deployment isn't advised because of security concerns.  

- **Set default keyboard layout in WinPE**: <!--4910348-->Configure the default keyboard layout for a boot image. If you select a language other than en-us, Configuration Manager still includes en-us in the available input locales. On the device, the initial keyboard layout is the selected locale, but the user can switch the device to en-us if needed.

> [!Tip]
> Use the [Set-CMBootImage](/powershell/module/configurationmanager/set-cmbootimage) PowerShell cmdlet to configure these settings from a script.

#### Optional Components

On the **Optional Components** tab, specify the components that are added to Windows PE for use with Configuration Manager. For more information about available optional components, see [WinPE: Add packages (Optional Components Reference)](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

The following components are required by Configuration Manager and always added to boot images:

- Scripting (WinPE-Scripting)
- Startup (WinPE-SecureStartup)
- Network (WinPE-WDS-Tools)
- Scripting (WinPE-WMI)

The **Components** list shows additional items that are added to this boot image. To add more components, select the gold asterisk. To remove a component, select it from the list, and then select the red X.

The following components are commonly used by customers:

- Microsoft .NET (WinPE-NetFX): This component is a prerequisite for PowerShell. It's one of the larger optional components.  
- Windows PowerShell (WinPE-PowerShell): This component requires .NET, and adds limited PowerShell support. If you run custom PowerShell scripts during the WinPE phase of your task sequence, add this component. There are other components that may be required for other PowerShell cmdlets.
- HTML (WinPE-HTA): If you run custom HTML applications during the WinPE phase of your task sequence, add this component.

For more information about adding languages, see [Configure multiple languages](#configure-multiple-languages).

#### Data Source

On the **Data Source** tab, update any of the following settings:  

- To change the source file of the boot image, set **Image path** and **Image index**.  

- To create a schedule for when the site updates the boot image, select **Update distribution points on a schedule**.  

- If you don't want the content of this package to age out of the client cache to make room for other content, select **Persist content in client cache**.  

- To specify that the site only distributes changed files when it updates the boot image package on the distribution point, select **Enable binary differential replication** (BDR). This setting minimizes the network traffic between sites. BDR is especially useful when the boot image package is large and the changes are relatively small.  

- If you use the boot image in a PXE-enabled deployment, select **Deploy this boot image from the PXE-enabled distribution point**. For more information, see [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

#### Data Access

On the **Data Access** tab, you can configure package share settings. If needed in your environment, set the option to **Copy the content in this package to a package share on distribution points**. You then have the additional option to **Use a custom name for the package share** and specify the custom **Share name**. Additional disk space is required on distribution points when you enable this option. It applies to all distribution points that receive this boot image.

#### Distribution Settings

On the **Distribution Settings** tab, select any of the following settings:  

- In the **Distribution priority** list, specify the priority level. Configuration Manager uses this priority list when the site distributes multiple packages to the same distribution point.  

- If you want to enable on-demand content distribution to preferred distribution points, select **Enable for on-demand distribution**. When you enable this setting, if a client requests the content for the package and the content isn't available on any distribution points, then the management point distributes the content. For more information, see [On-demand content distribution](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

- To specify how you want the site to distribute the boot image to distribution points that are enabled for prestaged content, set the **Prestaged distribution point settings**. For more information about prestaged content, see [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

#### Content Locations

On the **Content Locations** tab, select the distribution point or distribution point group, and use the following actions:  

- **Validate**: Check the integrity of the boot image package on the selected distribution point or distribution point group.  

- **Redistribute**: Distribute the boot image to the selected distribution point or distribution point group again.  

- **Remove**: Delete the boot image from the selected distribution point or distribution point group.  

#### Security

On the **Security** tab, view the administrative users that have permissions to this object.

## Configure a boot image for PXE

Before you can use a boot image for a PXE-based deployment, configure the boot image to deploy from a PXE-enabled distribution point.  

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Boot Images** node.  

2. Select the boot image that you want to modify.  

3. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.  

4. On the **Data Source** tab, select **Deploy this boot image from the PXE-enabled distribution point**. For more information, see [Use PXE to deploy Windows over the network](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## Configure multiple languages

> [!TIP]
> You can configure the default keyboard layout on the properties of a boot image. For more information, see [Customization](#customization).<!--4910348-->

Boot images are language neutral. This functionality allows you to use one boot image to display the task sequence text in multiple languages while in WinPE. Include the appropriate language support from the boot image **Optional Components** tab. Then set the appropriate task sequence variable to indicate which language to display. The language of the deployed OS is independent from the language in WinPE. The language that WinPE displays to the user is determined as follows:  

- When a user runs the task sequence from an existing OS, Configuration Manager automatically uses the language configured for the user. When the task sequence automatically runs as the result of a mandatory deployment deadline, Configuration Manager uses the language of the OS.  

- For OS deployments that use PXE or media, set the language ID value in the **SMSTSLanguageFolder** variable as part of a prestart command. When the computer boots to WinPE, messages are displayed in the language that you specified in the variable. If there's an error accessing the language resource file in the specified folder, or you don't set the variable, WinPE displays messages in the default language.  

    > [!NOTE]  
    > When you protect media with a password, the text that prompts the user for the password is always displayed in the WinPE language.  

Use the following procedure to set the WinPE language for PXE or media-initiated OS deployments.  

### Set the Windows PE language for a PXE or media-initiated OS deployment

1. Before you update the boot image, verify that the appropriate task sequence resource file (tsres.dll) is in the corresponding language folder on the site server. For example, the English resource file is in the following location: `<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. As part of your prestart command, set the **SMSTSLanguageFolder** environment variable to the appropriate language ID. The language ID must be specified by using decimal and not hexadecimal format. For example, to set the language ID to English, specify the decimal value **1033**, not the hexadecimal value 00000409 of the folder name.

## Next steps

[Customize boot images](customize-boot-images.md)

[Manage OS images](manage-operating-system-images.md)
