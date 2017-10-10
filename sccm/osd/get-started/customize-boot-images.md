---
title: "Customize boot images - Configuration Manager"
description: "Learn several ways to use Configuration Manager or the Deployment Image Servicing and Management (DISM) command-line tool to customize a boot image."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
caps.latest.revision: 15
caps.handback.revision: 0
author: Dougebyms.author: dougebymanager: angrobe

---
# Customize boot images with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Each version of Configuration Manager supports a specific version of the Windows Assessment and Deployment Kit (Windows ADK). You can service, or customize, boot images from the Configuration Manager console when they are based on a Windows PE  version from the supported version of Windows ADK. For other boot images, you must customize them by using another method, such as using the Deployment Image Servicing and Management (DISM) command-line tool that is part of the Windows AIK and Windows ADK.  

 The following provides the supported version of Windows ADK, the Windows PE version on which the boot image is based that can be customized from the Configuration Manager console, and the Windows PE versions on which the boot image is based that you can customize by using DISM and then add the image to Configuration Manager.  

-   **Windows ADK version**  

     Windows ADK for Windows 10  

-   **Windows PE versions for boot images customizable from the Configuration Manager console**  

     Windows PE 10  

-   **Supported Windows PE versions for boot images not customizable from the Configuration Manager console**  

     Windows PE 3.1<sup>1</sup> and Windows PE 5  

     <sup>1</sup> You can only add a boot image to Configuration Manager when it is based on Windows PE 3.1. Install the Windows AIK Supplement for Windows 7 SP1 to upgrade Windows AIK for Windows 7 (based on Windows PE 3) with the Windows AIK Supplement for Windows 7 SP1 (based on Windows PE 3.1). You can download Windows AIK Supplement for Windows 7 SP1 from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=5188).  

     For example, when you have Configuration Manager, you can customize boot images from Windows ADK for Windows 10 (based on Windows PE 10) from the Configuration Manager console. However, while boot images based on Windows PE 5 are supported, you must customize them from a different computer and use the version of DISM that is installed with Windows ADK for Windows 8. Then, you can add the boot image to the Configuration Manager console.  

 The procedures in this topic demonstrate how to add the optional components required by Configuration Manager to the boot image by using the following Windows PE packages:  

-   **WinPE-WMI**: Adds Windows Management Instrumentation (WMI) support.  

-   **WinPE-Scripting**: Adds Windows Script Host (WSH) support.  

-   **WinPE-WDS-Tools**: Installs Windows Deployment Services tools.  

 There are other Windows PE packages available for you to add. The following resources provide more information about the optional components that you can add to the boot image.  

-   For Windows PE 5, see [WinPE: Add packages (Optional Components Reference)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx)  

-   For Windows PE 3.1, see the [Add a Package to a Windows PE Image](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) topic in the Windows 7 TechNet Documentation Library.  

> [!NOTE]
>When you boot to WinPE from a customized boot image that includes tools that you added, you can open a command prompt from WinPE and type the file name of the tool to run it. The location of these tools are automatically added to the path variable. The command prompt can only be added if the **Enable command support (testing only)** setting is selected on the **Customization** tab in the boot image properties.

## Customize a boot image that uses Windows PE 5  
 To customize a boot image that uses Windows PE 5, you must install Windows ADK and use the DISM command-line tool to mount the boot image, add optional components and drivers, and commit the changes to the boot image. Use the following procedure to customize the boot image.  

#### To customize a boot image that uses Windows PE 5  

1.  Install the Windows ADK on a computer that does not have another version of Windows AIK or Windows ADK, and does not have any Configuration Manager components installed.  

2.  Download Windows ADK for Windows 8.1 from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=39982).  

3.  Copy the boot image (wimpe.wim) from the Windows ADK installation folder (for example, <*Installation path*>\Windows Kits\\<*version*>\Assessment and Deployment Kit\Windows Preinstallation Environment\\<*x86 or amd64*>\\<*locale*>) to a destination folder on the computer from which you will customize the boot image. This procedure uses C:\WinPEWAIK as the destination folder name.  

4.  Use DISM to mount the boot image to a local Windows PE folder. For example, type the following command-line:  

     **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     Where C:\WinPEWAIK is the folder that contains the boot image and C:\WinPEMount is the mounted folder.  

    > [!NOTE]
    >  For more information about DISM, see the [DISM - Deployment Image Servicing and Management Technical Reference](http://technet.microsoft.com/library/hh824821.aspx) topic in the Windows 8.1 and Windows 8 TechNet Documentation Library.

5.  After you mount the boot image, use DISM to add optional components to the boot image. In Windows PE 5, the 64-bit optional components are located in <*Installation path*>\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs.  

    > [!NOTE]
    >  This procedure uses the following location for the optional components: C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs. The path you use might be different depending on the version and installation options you choose for the Windows ADK.  

     Type the following to install the optional components:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-SecureStartup_** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-WMI_** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-Scripting** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-WDS-Tools_** *<locale\>* **.cab"**  

     Where C:\WinPEMount is the mounted folder and locale is the locale for the components. For example, for the **en-us** locale, you would type:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

    > [!TIP]
    >  For more information about the optional components that you can add to the boot image, see the [Windows PE Optional Components Reference](http://technet.microsoft.com/library/hh824926.aspx) topic in the Windows 8.1 and Windows 8 TechNet Documentation Library.  

6.  Use DISM to add specific drivers to the boot image, when required. Type the following to add drivers to the boot image:  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *path to driver .inf file* **>**  

     Where C:\WinPEMount is the mounted folder.  

7.  Type the following to unmount the boot image file and commit the changes.  

     **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     Where C:\WinPEMount is the mounted folder.  

8.  Add the updated boot image to Configuration Manager to make it available to use in your task sequences. Use the following steps to import the updated boot image:  

    1.  In the Configuration Manager console, click **Software Library**.  

    2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Boot Images**.  

    3.  On the **Home** tab, in the **Create** group, click **Add Boot Image** to start the Add Boot Image Wizard.  

    4.  On the **Data Source** page, specify the following options, and then click **Next**.  

        -   In the **Path** box, specify the path to the updated boot image file. The specified path must be a valid network path in the UNC format. For example:  **\\\\<***servername***>\\<***WinPEWAIK share***>\winpe.wim**.  

        -   Select the boot image from the **Boot Image** drop-down list. If the WIM file contains multiple boot images, each image is listed.  

    5.  On the **General** page, specify the following options, and then click **Next**.  

        -   In the **Name** box, specify a unique name for the boot image.  

        -   In the **Version** box, specify a version number for the boot image.  

        -   In the **Comment** box, specify a brief description of how the boot image is used.  

    6.  Complete the wizard.  

9. You can enable a command shell in the boot image to debug and troubleshoot it in Windows PE. Use the following steps to enable the command shell.  

    1.  In the Configuration Manager console, click **Software Library**.  

    2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Boot Images**.  

    3.  Find the new boot image in the list and identify the package ID for the image. You can find the package ID in the **Image ID** column for the boot image.  

    4.  From a command prompt, type **wbemtest** to open the Windows Management Instrumentation Tester.  

    5.  Type **\\\\<***SMS Provider Computer***>\root\sms\site_<***sitecode***>** in **Namespace**, and then click **Connect**.  

    6.  Click **Open Instance**, type **sms_bootimagepackage.packageID="<packageID\>"**, and then click **OK**. For packageID, enter the value that you identified in step 3.  

    7.  Click **Refresh Object**, and then click **EnableLabShell** in the **Properties** pane.  

    8.  Click **Edit Property**, change the value to **TRUE**, and click **Save Property**.  

    9. Click **Save Object**, and then exit the Windows Management Instrumentation Tester.  

10. You must distribute the boot image to distribution points, distribution point groups, or to collections that are associated with distribution point groups before you can use the boot image in a task sequence. Use the following steps to distribute the boot image.  

    1.  In the Configuration Manager console, click **Software Library**.  

    2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Boot Images**.  

    3.  Click the boot image identified in step 3.  

    4.  On the **Home** tab, in the **Deployment** group, click **Update Distribution Points**.  

## Customize a boot image that uses Windows PE 3.1  
 To customize a boot image that uses WinPE 3.1, you must install Windows AIK, install the Windows AIK supplement for Windows 7 SP1, and use the DISM command-line tool to mount the boot image, add optional components and drivers, and commit the changes to the boot image. Use the following procedure to customize the boot image.  

#### To customize a boot image that uses Windows PE 3.1  

1.  Install the Windows AIK on a computer that does not have another version of Windows AIK or Windows ADK, and does not have any Configuration Manager components installed. Download Windows AIK from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=5753).  

2.  Install the Windows AIK Supplement for Windows 7 with SP1 on the computer from step 1. Download Windows AIK Supplement for Windows 7 SP1 from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=5188).  

3.  Copy the boot image (wimpe.wim) from the Windows AIK installation folder (for example, <*InstallationPath*>\Windows AIK\Tools\PETools\amd64\\) to a folder on the computer from which you will customize the boot image. This procedure uses C:\WinPEWAIK as the folder name.  

4.  Use DISM to mount the boot image to a local Windows PE folder. For example, type the following command-line:  

     **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     Where C:\WinPEWAIK is the folder that contains the boot image and C:\WinPEMount is the mounted folder.  

    > [!NOTE]
    >  For more information about DISM, see the [Deployment Image Servicing and Management Technical Reference](http://technet.microsoft.com/library/dd744256\(v=ws.10\).aspx) topic in the Windows 7 TechNet Documentation Library.  

5.  After you mount the boot image, use DISM to add optional components to the boot image. In Windows PE 3.1, for example, the optional components are located in <*InstallationPath*>\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\.  

    > [!NOTE]
    >  This procedure uses the following location for the optional components: C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs. The path you use might be different depending on the version and installation options you choose for the Windows AIK.  

     Type the following to install the optional components:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-wmi_** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-scripting_** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-wds-tools_** *<locale\>* **.cab"**  

     Where C:\WinPEMount is the mounted folder and locale is the locale for the components. For example, for the **en-us** locale, you would type:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

    > [!TIP]
    >  For more information about the different packages that you can add to the boot image, see the [Add a Package to a Windows PE Image](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) topic in the Windows 7 TechNet Documentation Library.  

6.  Use DISM to add specific drivers to the boot image, when required. Type the following to add drivers to the boot image, if required:  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *path to driver .inf file* **>**  

     Where C:\WinPEMount is the mounted folder.  

7.  Type the following to unmount the boot image file and commit the changes.  

     **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     Where C:\WinPEMount is the mounted folder.  

8.  Add the updated boot image to Configuration Manager to make it available to use in your task sequences. Use the following steps to import the updated boot image:  

    1.  In the Configuration Manager console, click **Software Library**.  

    2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Boot Images**.  

    3.  On the **Home** tab, in the **Create** group, click **Add Boot Image** to start the Add Boot Image Wizard.  

    4.  On the **Data Source** page, specify the following options, and then click **Next**.  

        -   In the **Path** box, specify the path to the updated boot image file. The specified path must be a valid network path in the UNC format. For example:  **\\\\<***servername***>\\<***WinPEWAIK share***>\winpe.wim**.  

        -   Select the boot image from the **Boot Image** drop-down list. If the WIM file contains multiple boot images, each image is listed.  

    5.  On the **General** page, specify the following options, and then click **Next**.  

        -   In the **Name** box, specify a unique name for the boot image.  

        -   In the **Version** box, specify a version number for the boot image.  

        -   In the **Comment** box, specify a brief description of how the boot image is used.  

    6.  Complete the wizard.  

9. You can enable a command shell in the boot image to debug and troubleshoot it in Windows PE. Use the following steps to enable the command shell.  

    1.  In the Configuration Manager console, click **Software Library**.  

    2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Boot Images**.  

    3.  Find the new boot image in the list and identify the package ID for the image. You can find the package ID in the **Image ID** column for the boot image.  

    4.  From a command prompt, type **wbemtest** to open the Windows Management Instrumentation Tester.  

    5.  Type **\\\\<***SMS Provider Computer***>\root\sms\site_<***sitecode***>** in **Namespace**, and then click **Connect**.  

    6.  Click **Open Instance**, type **sms_bootimagepackage.packageID="<packageID\>"**, and then click **OK**. For packageID, enter the value that you identified in step 3.  

    7.  Click **Refresh Object**, and then click **EnableLabShell** in the **Properties** pane.  

    8.  Click **Edit Property**, change the value to **TRUE**, and click **Save Property**.  

    9. Click **Save Object**, and then exit the Windows Management Instrumentation Tester.  

10. You must distribute the boot image to distribution points, distribution point groups, or to collections that are associated with distribution point groups before you can use the boot image in a task sequence. Use the following steps to distribute the boot image.  

    1.  In the Configuration Manager console, click **Software Library**.  

    2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Boot Images**.  

    3.  Click the boot image identified in step 3.  

    4.  On the **Home** tab, in the **Deployment** group, click **Update Distribution Points**.  
