---
title: Customize boot images
titleSuffix: Configuration Manager
description: Learn several ways to use Configuration Manager or the Deployment Image Servicing and Management (DISM) command-line tool to customize a boot image.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Customize boot images with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Each version of Configuration Manager supports a specific version of the Windows Assessment and Deployment Kit (Windows ADK). You can service, or customize, boot images from the Configuration Manager console when they're based on a Windows PE (WinPE) version from the supported version of Windows ADK. For other boot images, you must customize them by using another method, such as using the Deployment Image Servicing and Management (DISM) command-line tool that is part of the Windows AIK and Windows ADK.

If you use a [supported version of the Windows ADK](../../core/plan-design/configs/support-for-windows-adk.md), you can customize those boot images in the Configuration Manager console. For more information on how to customize boot images in the Configuration Manager console, see [Manage boot images](manage-boot-images.md#modify-a-boot-image).

Configuration Manager also supports boot images based on **Windows PE version 3.1**. However, you can't customize these boot images in the Configuration Manager console.

For example, you can customize boot images based on Windows PE 10 from the Windows ADK for Windows 10 from the Configuration Manager console. However, while boot images based on Windows PE 3.1 are supported, you need to customize them from a different computer and use the version of DISM that's installed with the Windows AIK for Windows 7. Then, you can add the boot image to the Configuration Manager console.

The procedures in this article demonstrate how to add the optional components required by Configuration Manager to the boot image by using the following Windows PE packages:

- **WinPE-WMI**: Adds Windows Management Instrumentation (WMI) support.

- **WinPE-Scripting**: Adds Windows Script Host (WSH) support.

- **WinPE-WDS-Tools**: Installs Windows Deployment Services tools.

There are other Windows PE packages available for you to add. For more information about the optional components that you can add to the boot image, see [WinPE: Add packages (Optional Components Reference)](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).

> [!NOTE]
> When you boot to WinPE from a customized boot image that includes tools that you added, you can open a command prompt from WinPE and type the file name of the tool to run it. The location of these tools are automatically added to the path variable. The command prompt can only be added if the **Enable command support (testing only)** setting is selected on the **Customization** tab in the boot image properties.

To customize a boot image that uses WinPE 3.1:

- Install the Windows AIK
- Install the Windows AIK supplement for Windows 7 SP1
- Use the DISM command-line tool to mount the boot image, add optional components and drivers, and commit the changes to the boot image.

1. Install the Windows AIK on a computer that doesn't have another version of the Windows AIK or Windows ADK, and doesn't have any Configuration Manager components installed. Download the Windows AIK from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5753).

1. Install the Windows AIK Supplement for Windows 7 with SP1 on the same computer. Download the Windows AIK Supplement for Windows 7 SP1 from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188).

1. Copy the boot image (wimpe.wim) from the Windows AIK installation folder `C:\Program Files\Windows AIK\Tools\PETools\amd64` to a folder on the computer where you'll customize the boot image. This procedure uses `C:\WinPEWAIK` as the folder name.

1. Create a new folder to use as the mount point for the boot image. This procedure uses `C:\WinPEMount` as the folder name.

1. Use DISM to mount the boot image to a local Windows PE folder. For example, type the following command line:

    `dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount`

    > [!NOTE]
    > For more information, see the [DISM (Deployment Image Servicing and Management) Reference](/windows-hardware/manufacture/desktop/dism-reference--deployment-image-servicing-and-management).

1. After you mount the boot image, use DISM to add optional components to the boot image. In Windows PE 3.1, for example, the optional components are located in `C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\`.

    > [!NOTE]
    > This procedure uses the following location for the optional components: `C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs`. The path you use might be different depending on the version and installation options you choose for the Windows AIK.

    Type the following commands to install the optional components:

    ```Command
    dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"

    dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"

    dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"

    dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"

    dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"

    dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"
    ```

    > [!NOTE]
    > These examples uses the **en-us** locale. You may need to change these locale strings in your environment.
    >
    > For more information about the different packages that you can add to the boot image, see [WinPE Optional Components (OC) Reference](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).

1. If needed, use DISM to add specific drivers to the boot image. For example, type the following command to add drivers to the boot image:

    `dism.exe /image:C:\WinPEMount /add-driver /driver:C:\Drivers\driver.inf`

1. Type the following command to unmount the boot image file and commit the changes:

    `dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit`

1. Add the updated boot image to Configuration Manager to make it available to use in your task sequences. Use the following steps to import the updated boot image:

    1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and select the **Boot Images** node.

    1. On the **Home** tab of the ribbon, in the **Create** group, select **Add Boot Image**. This action starts the Add Boot Image Wizard.

    1. On the **Data Source** page, specify the following options:

        - Specify the **Path** to the updated boot image file. The specified path must be a valid network path in the UNC format. For example: `\\server\WinPEWAIK\winpe.wim`

        - Choose the specific boot image from the **Boot Image** list. If the WIM file contains multiple images, each image is listed.

    1. On the **General** page, specify the following options:

        - **Name**: Specify a unique name for the boot image.

        - **Version**: Specify a version number for the boot image. This value doesn't have to be the OS version, it's a string that you maintain for the boot image version.

        - **Comment**: Specify an optional description of how the boot image is used to better identify it in the console.

    1. Complete the wizard.

1. You can enable a command shell in the boot image to open a command prompt by using the **F8** key while the boot image is deployed. This option is useful for troubleshooting while you're testing your deployment. Using this setting in a production deployment isn't advised because of security concerns. Use the following steps to enable the command shell:

    1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Boot Images** node.

    1. Find the new boot image in the list and identify the package ID for the image. You can find the package ID in the **Image ID** column for the boot image.

    1. From a command prompt, type `wbemtest` to open the Windows Management Instrumentation Tester.

    1. For the **Namespace**, type `\\<smsprovider>\root\sms\site_<sitecode>`, and then select **Connect**.

    1. Select **Open Instance**. Type `sms_bootimagepackage.packageID="<packageID>"`, and then select **OK**.

    1. Select **Refresh Object**, and then in the **Properties** pane select **EnableLabShell**.

    1. Select **Edit Property**, change the value to **TRUE**, and select **Save Property**.

    1. Select **Save Object**, and then exit the Windows Management Instrumentation Tester.

1. Before you can use the boot image in a task sequence, distribute the boot image to distribution points. Use the following steps to distribute the boot image:

    1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Boot Images** node.

    1. Select the new boot image based on Windows PE 3.1.

    1. On the **Home** tab of the ribbon, in the **Deployment** group, select **Update Distribution Points**.
