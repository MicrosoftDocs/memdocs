---
title: Customize boot images
titleSuffix: Configuration Manager
description: Learn several ways to use Configuration Manager or the Deployment Image Servicing and Management (DISM) command-line tool to customize a boot image.
ms.date: 12/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Customize boot images with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Each version of Configuration Manager supports a specific version of the Windows Assessment and Deployment Kit (Windows ADK). You can service, or customize, boot images from the Configuration Manager console when they're based on a Windows PE (WinPE) version from the WinPE add-on of a [supported version of the Windows ADK](../../core/plan-design/configs/support-for-windows-adk.md). For more information on how to customize boot images in the Configuration Manager console, see [Manage boot images](manage-boot-images.md#modify-a-boot-image).

For boot images with other versions of WinPE, customize them by using another method. For example, use the Deployment Image Servicing and Management (DISM) command-line tool. Then import the boot images into Configuration Manager to use with OS deployments.

For example, you install the Windows ADK and WinPE add-on for Windows 11 on the site server. For x64 boot images based on WinPE version 11 from the WinPE add-on for Windows 11, you can customize them from the Configuration Manager console. However, while x86 boot images based on WinPE version 10 are supported, you need to manually customize them from a different computer. Use the version of DISM that's installed with the Windows ADK for Windows 10. Then, you can add the boot image to the Configuration Manager console.

> [!IMPORTANT]
> The 32-bit versions of Windows PE (WinPE) in the WinPE add-ons for Windows 11 and Windows Server 2022 aren't supported. The last supported version of 32-bit WinPE is available in the **WinPE add-on for Windows 10, version 2004**. For more information, see [Download and install the Windows ADK](/windows-hardware/get-started/adk-install).<!--12440724--><!-- the same text of this note is also used in the include file: ../../core/plan-design/configs/includes/windows11-adk-x86.md -->

The following steps summarize the process to customize an x86 boot image that uses WinPE version 10:

- Install the Windows ADK and WinPE add-on for Windows 10, version 2004
- Use the DISM command-line tool to:
  - Mount the x86 boot image
  - Add optional components
  - Add drivers
  - Commit the changes to the boot image
- Import the customized boot image to Configuration Manager

## Required components

The procedures in this article demonstrate how to add the WinPE _optional components_ that Configuration Manager requires:

- **WinPE-WMI**: Adds Windows Management Instrumentation (WMI) support.

- **WinPE-Scripting**: Adds Windows Script Host (WSH) support.

- **WinPE-WDS-Tools**: Installs Windows Deployment Services (WDS) tools.

There are other WinPE packages available to add. For more information, see [WinPE optional components reference](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).

## Customize the image with DISM

1. On a computer that doesn't have a version of the Windows ADK and doesn't have any Configuration Manager components installed, install the Windows ADK (`adksetup.exe`) and WinPE add-on (`adkwinpesetup.exe`). For more information, see [Other ADK downloads](/windows-hardware/get-started/adk-install#other-adk-downloads).

    > [!TIP]
    > You only need to install the **Deployment Tools** component for this process.

1. Copy the boot image (`winpe.wim`) from the WinPE installation folder, which by default is `C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\x86\en-us`. Create a working directory on the computer where you'll customize the boot image, and copy the default image file to it. This procedure uses `C:\WinPE` as the folder name. For example:

    ```powershell
    $workingDir = New-Item -Path "C:\" -Name "WinPE" -ItemType "directory"
    $peDir = "C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\x86\en-us"
    Copy-Item "$($peDir)\winpe.wim" -Destination $workingDir
    ```

1. Create a new folder to use as the mount point for the boot image. This procedure uses `C:\WinPEMount` as the folder name.

    ```powershell
    New-Item -Path "C:\" -Name "WinPEMount" -ItemType "directory"
    ```

1. Use DISM to mount the boot image to a local Windows PE folder. For example, type the following command line:

    > [!IMPORTANT]
    > Make sure you're using the version of DISM from the installed Windows ADK. Windows may default to the OS version, which may not technically support the version of WinPE that you're servicing. For more information, see [DISM supported platforms](/windows-hardware/manufacture/desktop/dism-supported-platforms).

    ```powershell
    Set-Location "C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools\amd64\DISM\"

    .\dism.exe /mount-wim /wimfile:C:\WinPE\winpe.wim /index:1 /mountdir:C:\WinPEMount
    ```

    > [!TIP]
    > For more information on DISM commands, see the [DISM Reference](/windows-hardware/manufacture/desktop/dism-reference--deployment-image-servicing-and-management).

1. After you mount the boot image, use DISM to add optional components to the boot image. By default, the optional components are located in `C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\x86\WinPE_OCs`.

    > [!NOTE]
    > This procedure uses the default location and `en-us` locale for the optional components. The path you use might be different depending on the version and installation options you choose for the Windows ADK, and the locale of the boot image.

    Type the following commands to install the optional components that Configuration Manager requires:

    ```powershell
    $ocpath = "C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\x86\WinPE_OCs"

    .\dism.exe /image:C:\WinPEMount /add-package /packagepath:"$($ocpath)\winpe-wmi.cab"

    .\dism.exe /image:C:\WinPEMount /add-package /packagepath:"$($ocpath)\winpe-scripting.cab"

    .\dism.exe /image:C:\WinPEMount /add-package /packagepath:"$($ocpath)\winpe-wds-tools.cab"

    .\dism.exe /image:C:\WinPEMount /add-package /packagepath:"$($ocpath)\en-us\winpe-wmi_en-us.cab"

    .\dism.exe /image:C:\WinPEMount /add-package /packagepath:"$($ocpath)\en-us\winpe-scripting_en-us.cab"

    .\dism.exe /image:C:\WinPEMount /add-package /packagepath:"$($ocpath)\en-us\winpe-wds-tools_en-us.cab"
    ```

    > [!TIP]
    > For more information about the different packages that you can add to the boot image, see [WinPE optional components reference](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).

1. If needed, use DISM to add specific drivers to the boot image. For example, type the following command to add a driver to the boot image:

    ```powershell
    .\dism.exe /image:C:\WinPEMount /add-driver /driver:C:\Drivers\driver.inf
    ```

1. When you're done making changes, type the following command to unmount the boot image file and commit the changes:

    ```powershell
    .\dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit
    ```

    > [!IMPORTANT]
    > Whether or not you will use this customized image, make sure to unmount it when you're done. To not save your changes but still unmount the image, use the `/discard` parameter instead of the `/commit` option.

1. Copy the customized boot image to your site's centralized package source location.

## Import the boot image

Add the updated boot image to Configuration Manager to make it available to use in your task sequences. Use the following steps to import the updated boot image:

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and select the **Boot Images** node.

1. On the **Home** tab of the ribbon, in the **Create** group, select **Add Boot Image**. This action starts the Add Boot Image Wizard.

1. On the **Data Source** page, specify the following options:

    - Specify the **Path** to the updated boot image file. The specified path must be a valid network path in the UNC format. For example: `\\server\share\WinPE10x86\winpe.wim`

    - Choose the specific boot image from the **Boot Image** list. If the WIM file contains multiple images, each image is listed.

1. On the **General** page, specify the following options:

    - **Name**: Specify a unique name for the boot image.

    - **Version**: Specify a version number for the boot image. This value doesn't have to be the OS version, it's a string that you maintain for the boot image version.

    - **Comment**: Specify an optional description of how the boot image is used to better identify it in the console.

1. Complete the wizard.

## Enable command shell for testing

You can enable a command shell in the boot image to open a command prompt by using the **F8** key while the boot image is deployed. This option is useful for troubleshooting while you're testing your deployment. Using this setting in a production deployment isn't advised because of security concerns.

Use the following steps to enable the command shell on a custom boot image:

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Boot Images** node.

1. Find the new boot image in the list and identify the package ID for the image. You can find the package ID in the **Image ID** column for the boot image.

1. From a command prompt, type `wbemtest` to open the Windows Management Instrumentation Tester.

1. For the **Namespace**, type `\\<smsprovider>\root\sms\site_<sitecode>`, and then select **Connect**.

1. Select **Open Instance**. Type `sms_bootimagepackage.packageID="<packageID>"`, and then select **OK**.

1. Select **Refresh Object**, and then in the **Properties** pane select **EnableLabShell**.

1. Select **Edit Property**, change the value to **TRUE**, and select **Save Property**.

1. Select **Save Object**, and then exit the Windows Management Instrumentation Tester.

> [!NOTE]
> When you boot to WinPE from a customized boot image that includes tools that you added, you can open a command prompt from WinPE and type the file name of the tool to run it. The location of these tools are automatically added to the path variable.

## Distribute content

Before you can use the boot image in a task sequence, distribute the boot image to distribution points. Use the following steps to distribute the boot image:

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Boot Images** node.

1. Select the new custom boot image.

1. On the **Home** tab of the ribbon, in the **Deployment** group, select **Update Distribution Points**.

## Next steps

[Manage boot images](manage-boot-images.md)

[Support for the Windows ADK in Configuration Manager](../../core/plan-design/configs/support-for-windows-adk.md)
