---
title: "Deploy Windows to Go"
titleSuffix: "Configuration Manager"
description: "Learn how to provision Windows To Go in System Center Configuration Manager to create a Windows To Go workspace that boots from an external drive."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
caps.latest.revision: 8
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: angrobe

---
# Deploy Windows to Go with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This topic provides the steps to provision Windows To Go in System Center Configuration Manager. Windows To Go is an enterprise feature of Windows 8 that enables the creation of a Windows To Go workspace that can be booted from a USB-connected external drive on computers that meet the Windows 7 or Windows 8 certification requirements, regardless of the operating system running on the computer. Windows To Go workspaces can use the same image enterprises use for their desktops and laptops and can be managed the same way.  

 For more information about Windows To Go, see [Windows To Go feature overview](http://go.microsoft.com/fwlink/p/?LinkId=263433).  

## Provision Windows To Go  
 Windows To Go is an operating system stored on a USB-connected external drive. You can provision the Windows To Go drive much like you provision other operating system deployments. However, because Windows To Go is designed to be a user-centric and highly mobile solution, you must take a slightly different approach to provisioning these drives.  

 At a high level, Windows To Go is a two-phased deployment that allows you to configure the Windows To Go device and prestage content for the operating system deployment. You can achieve this with minimal impact to the user and limit downtime for the user's computer. After you prestage the computer, you must complete the provisioning process to ensure the computer is ready for the user. The provisioning process is similar to the current operating system deployment process. The following lists the general workflow to prestage content and provision Windows To Go:  

1.  [Prerequisites to provision Windows To Go](#BKMK_Prereqs)  

2.  [Create prestaged media](#BKMK_CreatePrestagedMedia)  

3.  [Create a Windows To Go Creator package](#BKMK_CreatePackage)  

4.  [Update the task sequence to enable BitLocker for Windows To Go](#BKMK_UpdateTaskSequence)  

5.  [Deploy the Windows To Go Creator package and task sequence](#BKMK_Deployments)  

6.  [User runs the Windows To Go Creator](#BKMK_UserExperience)  

7.  [Configuration Manager configures and stages the Windows To Go drive](#BKMK_ConfigureStageDrive)  

8.  [User logs in to Windows 8](#BKMK_UserLogsIn)  

###  <a name="BKMK_Prereqs"></a> Prerequisites to provision Windows To Go  
 Before you provision Windows To Go, you must complete the following in Configuration Manager:  

-   **Distribute a boot image to a distribution point**  

     Before you create prestaged media, you must distribute the boot image to a distribution point.  

    > [!NOTE]  
    >  Boot images are used to install the operating system on the destination computers in your Configuration Manager environment. They contain a version of Windows PE that installs the operating system, as well as any additional device drivers that are required. Configuration Manager provides two boot images: One to support x86 platforms and one to support x64 platforms. You can also create your own boot images. For more information, see [Manage boot images](../get-started/manage-boot-images.md).  

-   **Distribute the Windows 8 operating system image to a distribution point**  

     Before you create prestaged media, you must distribute the Windows 8 operating system image to a distribution point.  

    > [!NOTE]  
    >  Operating system images are .WIM format files and represent a compressed collection of reference files and folders that are required to successfully install and configure an operating system on a computer. For more information, see [Manage operating system images](../get-started/manage-operating-system-images.md).  

-   **Create a Task Sequence to Deploy Windows 8**  

     You must create a task sequence for a Windows 8 deployment that you will reference when you create prestaged media. For more information, see [Manage task sequences to automate tasks](manage-task-sequences-to-automate-tasks.md).  

###  <a name="BKMK_CreatePrestagedMedia"></a> Create prestaged media  
 Prestaged media contains the boot image used to start the destination computer and the operating system image that is applied to the destination computer. The computer that you provision with prestaged media can be started by using the boot image. The computer can then run an existing operating system deployment task sequence to install a complete operating system deployment. The task sequence that deploys the operating system is not included in the media.  

 You can add content, such as applications and device drivers, in addition to the operating system image and boot image during the prestage phase. This reduces the time it takes to deploy an operating system and reduces network traffic because the content is already on the drive.  

 Use the following procedure to create the prestaged media.  

#### To create prestaged media  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  On the **Home** tab, in the **Create** group, click **Create Task Sequence Media** to start the Create Task Sequence Media Wizard.  

4.  On the **Select Media Type** page, specify the following information, and then click **Next**.  

    -   Select **Prestaged media**.  

    -   Select **Allow unattended operating system deployment** to boot to the Windows To Go deployment with no user interaction.  

        > [!IMPORTANT]  
        >  When you use this option with the SMSTSPreferredAdvertID custom variable (set later in this procedure), no user interaction is required and the computer will automatically boot to the Windows To Go deployment when it detects a Windows To Go drive. The user is still prompted for a password if the media is configured for password protection. If you use the **Allow unattended operating system deployment** setting without configuring the SMSTSPreferredAdvertID variable, an error will occur when you deploy the task sequence.  

5.  On the **Media Management** page, specify the following information, and then click **Next**.  

    -   Select **Dynamic media** if you want to allow a management point to redirect the media to another management point, based on the client location in the site boundaries.  

    -   Select **Site-based media** if you want the media to contact only the specified management point.  

6.  On the **Media Properties**  page, specify the following information, and then click **Next**.  

    -   **Created by**: Specify who created the media.  

    -   **Version**: Specify the version number of the media.  

    -   **Comment**: Specify a unique description of what the media is used for.  

    -   **Media file**: Specify the name and path of the output files. The wizard writes the output files to this location. For example: **\\\servername\folder\outputfile.wim**  

7.  On the **Security** page, specify the following information, and then click **Next**.  

    -   Select **Enable unknown computer support** to allow the media to deploy an operating system to a computer that is not managed by Configuration Manager. There is no record of these computers in the Configuration Manager database. Unknown computers include the following:  

        -   A computer where the Configuration Manager client is not installed  

        -   A computer that is not imported into Configuration Manager  

        -   A computer that is not discovered by Configuration Manager  

    -   Select **Protect the media with a password** and enter a strong password to help protect the media from unauthorized access. When you specify a password, the user must provide that password to use the prestaged media.  

        > [!IMPORTANT]  
        >  As a security best practice, always assign a password to help protect the prestaged media.  

        > [!NOTE]  
        >  When you protect the prestaged media with a password, the user is prompted for the password even when the media is configured with the **Allow unattended operating system deployment** setting.  

    -   For HTTP communications, select **Create self-signed media certificate**, and then specify the start and expiration date for the certificate.  

    -   For HTTPS communications, select **Import PKI certificate**, and then specify the certificate to import and its password.  

         For more information about this client certificate that is used for boot images, see [PKI certificate requirements](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **User Device Affinity**: To support user-centric management in Configuration Manager, specify how you want the media to associate users with the destination computer. For more information about how operating system deployment supports user device affinity, see [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md).  

        -   Specify **Allow user device affinity with auto-approval** if you want the media to automatically associate users with the destination computer. This functionality is based on the actions of the task sequence that deploys the operating system. In this scenario, the task sequence creates a relationship between the specified users and destination computer when it deploys the operating system to the destination computer.  

        -   Specify **Allow user device affinity pending administrator approval** if you want the media to associate users with the destination computer after approval is granted. This functionality is based on the scope of the task sequence that deploys the operating system. In this scenario, the task sequence creates a relationship between the specified users and the destination computer, but waits for approval from an administrative user before the operating system is deployed.  

        -   Specify **Do not allow user device affinity** if you do not want the media to associate users with the destination computer. In this scenario, the task sequence does not associate users with the destination computer when it deploys the operating system.  

8.  On the **Task Sequence** page, specify the Windows 8 task sequence that you created in the previous section.  

9. On the **Boot image** page, specify the following information, and then click **Next**.  

    > [!IMPORTANT]  
    >  The architecture of the boot image that is distributed must be appropriate for the architecture of the destination computer. For example, an x64 destination computer can boot and run an x86 or x64 boot image. However, an x86 destination computer can boot and run only an x86 boot image. For Windows 8 certified computers in EFI mode, you must use an x64 boot image.  

    -   **Boot image**: Specify the boot image to start the destination computer.  

    -   **Distribution point**: Specify the distribution point that hosts the boot image. The wizard retrieves the boot image from the distribution point and writes it to the media.  

        > [!NOTE]  
        >  The administrative user must have **Read** access rights to the boot image content on the distribution point. For more information, see [Manage accounts to access content](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).  

    -   If you selected **Site-based media** on the **Media Management** page of this wizard, in the **Management point** box, specify a management point from a primary site.  

    -   If you selected **Dynamic media** on the **Media Management** page of the wizard, in the **Associated management points** box, specify the primary site management points to use and a priority order for the initial communications.  

10. On the **Images** page, specify the following information, and then click **Next**.  

    -   **Image package**: Specify the package that contains the Windows 8 operating system image.  

    -   **Image index**: Specify the image to deploy if the package contains multiple operating system images.  

    -   **Distribution point**: Specify the distribution point that hosts the operating system image package. The wizard retrieves the operating system image from the distribution point and writes it to the media.  

        > [!NOTE]  
        >  The administrative user must have **Read** access rights to the operating system image content on the distribution point. For more information, see [Manage accounts to access content](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).  

11. On the **Select Application** page, select application content to include in the media file, and then click **Next**.  

12. On the **Select Package** page, select additional package content to include in the media file, and then click **Next**.  

13. On the **Select Driver Package** page, select driver package content to include in the media file, and then click **Next**.  

14. On the **Distribution Points** page, select one or more distribution points that contain the content required by the task sequence, and then click **Next**.  

15. On the **Customization** page, specify the following information, and then click **Next**.  

    -   **Variables**: Specify the variables that the task sequence uses to deploy the operating system. For Windows To Go, use the SMSTSPreferredAdvertID variable to automatically select the Windows To Go deployment by using the following format:  

         SMSTSPreferredAdvertID = {*DeploymentID*}, where DeploymentID is the deployment ID associated with the task sequence that you will use to complete the provisioning process for the Windows To Go drive.  

        > [!TIP]  
        >  When you use this variable with a task sequence that is set to run unattended (set earlier in this procedure), no user interaction is required and the computer automatically boots to the Windows To Go deployment when it detects a Windows To Go drive. The user is still prompted for a password if the media is configured for password protection.  

    -   **Prestart commands**: Specify any prestart commands that you want to run before the task sequence runs. Prestart commands can be a script or executable that can interact with the user in Windows PE before the task sequence runs to install the operating system. Configure the following for the Windows To Go deployment:  

        -   **OSDBitLockerPIN**: BitLocker for Windows To Go requires a passphrase. Set the **OSDBitLockerPIN** variable as part of a prestart command to set the BitLocker passphrase for the Windows To Go drive.  

            > [!WARNING]  
            >  After BitLocker is enabled for the passphrase, the user must enter the passphrase each time the computer boots to the Windows To Go drive.  

        -   **SMSTSUDAUsers**: Specifies the primary user of the destination computer. Use this variable to collect the user name, which can then be used to associate the user and device. For more information, see [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md).  

            > [!TIP]  
            >  To retrieve the username, you can create an input box as part of the prestart command, have the user enter their username, and then set the variable with the value. For example, you can add the following lines to the prestart command script file:  
            >   
            >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
            >   
            >  `env("SMSTSUDAUsers") = UserID`  

         For more information about how to create a script file to use as your prestart command, see [Prestart commands for task sequence media](../understand/prestart-commands-for-task-sequence-media.md).  

16. Complete the wizard.  

    > [!NOTE]  
    >  It can take an extended period of time for the wizard to complete the prestaged media file.  

###  <a name="BKMK_CreatePackage"></a> Create a Windows To Go Creator package  
 As part of the Windows To Go deployment, you must create a package to deploy the prestage media file. The package must include the tool that configures the Windows To Go drive and extracts the prestaged media to the drive. Use the following procedure to create the Windows To Go Creator package.  

#### To create the Windows To Go Creator package  

1.  On the server to host the Windows To Go Creator package files, create a source folder for the package source files.  

    > [!NOTE]  
    >  The computer account of the site server must have **Read** access rights to the source folder.  

2.  Copy the prestaged media file that you created in the [Create prestaged media](#BKMK_CreatePrestagedMedia) section to the package source folder.  

3.  Copy the Windows To Go Creator tool (WTGCreator.exe) to the package source folder. The creator tool is available on any primary site server at the following location: <*ConfigMgrInstallationFolder*>\OSD\Tools\WTG\Creator.  

4.  Create a package and program by using the Create Package and Program Wizard.  

5.  In the Configuration Manager console, click **Software Library**.  

6.  In the **Software Library** workspace, expand **Application Management**, and then click **Packages**.  

7.  On the **Home** tab, in the **Create** group, click **Create Package**.  

8.  On the **Package** page, specify the name and description of the package. For example, enter **Windows To Go** for the package name and specify **Package to configure a Windows To Go drive using System Center Configuration Manager** for the package description.  

9. Select **This package contains source files**, specify the path to the package source folder that you created in step 1, and then click **Next**.  

10. On the **Program Type** page, select **Standard program**, and then click **Next**.  

11. On the **Standard Program** page, specify the following:  

    -   **Name**: Specify the name of the program. For example, type **Creator** for the program name.  

    -   **Command Line**: Type **WTGCreator.exe /wim:PrestageName.wim**, where PrestageName is the name of prestaged file that you created and copied to the package source folder for the Windows To Go Creator package.  

         Optionally, you can add the following options:  

        -   **enableBootRedirect**: command-line option to change the Windows To Go startup options to allow boot redirection. When you use this option, the computer will boot from USB without having to change the boot order in the computer firmware or have the user select from a list of boot options during startup. If a Windows To Go drive is detected, the computer boots to that drive.  

    -   **Run**: Specify **Normal** to run the program based on the system and program defaults.  

    -   **Program can run**: Specify whether the program can run only when a user is logged on.  

    -   **Run mode**: Specify whether the program will run with the logged on users permissions or with administrative permissions. The Windows To Go Creator requires elevated permissions to run.  

    -   Select **Allow users to view and interact with the program installation**, and then click **Next**.  

12. On the Requirements page, specify the following:  

    -   **Platform requirements**: Select the applicable Windows 8 platforms to allow provisioning.  

    -   **Estimated disk space**: Specify the size of the package source folder for the Windows To Go Creator.  

    -   **Maximum allowed run time (minutes)**: Specifies the maximum time that the program is expected to run on the client computer. By default, this value is set to 120 minutes.  

        > [!IMPORTANT]  
        >  If you are using maintenance windows for the collection on which this program is run, a conflict might occur if the **Maximum allowed run time** is longer than the scheduled maintenance window. If the maximum run time is set to **Unknown**, it will start during the maintenance window, but will continue to run until it completes or fails after the maintenance window is closed. If you set the maximum run time to a specific period (not set to Unknown) that exceeds the length of any available maintenance window, then that program will not be run.  

        > [!NOTE]  
        >  If the value is set to **Unknown**, Configuration Manager sets the maximum allowed run time to 12 hours (720 minutes).  

        > [!NOTE]  
        >  If the maximum run time (whether set by the user or as the default value) is exceeded, Configuration Manager stops the program if **run with administrative rights** is selected and **Allow users to view and interact with the program installation** is not selected on the **Standard Program** page.  

     Click **Next** and complete the wizard.  

###  <a name="BKMK_UpdateTaskSequence"></a> Update the task sequence to enable BitLocker for Windows To Go  
 Windows To Go enables BitLocker on an external bootable drive without the use of TPM. Therefore, you must use a separate tool to configure BitLocker on the Windows To Go drive. To enable BitLocker, you must add an action to the task sequence after the **Setup Windows and ConfigMgr** step.  

> [!NOTE]  
>  BitLocker for Windows To Go requires a passphrase. In the [Create prestaged media](#BKMK_CreatePrestagedMedia) step, you set the passphrase as part of a prestart command by using the OSDBitLockerPIN variable.  

 Use the following procedure to update the Windows 8 task sequence to enable BitLocker for Windows To Go.  

#### To update the Windows 8 task sequence to enable BitLocker  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Application Management**, and then click **Packages**.  

3.  On the **Home** tab, in the **Create** group, click **Create Package**.  

4.  On the **Package** page, specify the name and description of the package. For example, type **BitLocker for Windows To Go** for the package name and specify **Package to update BitLocker for Windows To Go** for the package description.  

5.  Select **This package contains source files**, specify the location for the BitLocker tool for Windows To Go, and then click **Next**. The BitLocker tool is available on any Configuration Manager primary site server at the following location: <*ConfigMgrInstallationFolder*>\OSD\Tools\WTG\BitLocker\  

6.  On the **Program Type** page, select **Do not create a program**.  

7.  Click **Next** and complete the wizard.  

8.  In the Configuration Manager console, click **Software Library**.  

9. In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

10. Select the Windows 8 task sequence that you reference in the prestaged media.  

11. On the **Home** tab, in the **Task Sequence** group, click **Edit**.  

12. Click the **Setup Windows and ConfigMgr** step, click **Add**, click **General**, and then click **Run Command Line**. The Run Command Line step is added after the Setup Windows and ConfigMgr step.  

13. On the **Properties** tab for the **Run Command Line** step, add the following:  

    1.  **Name**: Specify a name for the command line, such as **Enable BitLocker for Windows To Go**.  

    2.  **Command Line**: i386\osdbitlocker_wtg.exe /Enable /pwd:< *None&#124;AD*>  

         Parameters:  

        -   /pwd:<None&#124;AD> - Specify the BitLocker password recovery mode. This parameter is required you use the /Enable parameter is in the command-line.  

             Select **AD** to configure BitLocker Drive Encryption to back up recovery information for BitLocker-protected drives to Active Directory Domain Services (AD DS). Backing up recovery passwords for a BitLocker-protected drive allows administrative users to recover the drive if it is locked. This ensures that encrypted data belonging to the enterprise can always be accessed by authorized users. When you specify **None**, the user is responsible for keeping a copy of the recovery password or recovery key. If the user loses that information or neglects to decrypt the drive before leaving the organization, administrative users cannot easily access to the drive.  

        -   /wait:<TRUE&#124;FALSE> - Specify whether the task sequence waits for encryption to complete before it completes.  

    3.  Select **Package**, and then specify the package that you created at the start of this procedure.  

    4.  On the **Options** tab, add the following conditions:  

        -   Condition = Task Sequence Variable  

        -   Variable = _SMSTSWTG  

        -   Condition = Equals  

        -   Value = True  

    > [!NOTE]  
    >  The **Enable BitLocker** step, which is likely after the new command-line step, is not used to enable BitLocker for Windows To Go. However, you can keep this step in the task sequence to use for Windows 8 deployments that do not use a Windows To Go drive.  

###  <a name="BKMK_Deployments"></a> Deploy the Windows To Go Creator package and task sequence  
 Windows To Go is a hybrid deployment process. Therefore, you must deploy the Windows To Go Creator package and the Windows 8 task sequence. Use the following procedures to complete the deployment process.  

#### To deploy the Windows To Go Creator package  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Application Management**, and then click **Packages**.  

3.  Select the Windows To Go package that you created in the [Create a Windows To Go Creator package](#BKMK_CreatePackage) step.  

4.  On the **Home** tab, in the **Deployment** group, click **Deploy**.  

5.  On the **General** page, specify the following settings:  

    1.  **Software**: Verify that the Windows To Go package is selected.  

    2.  **Collection**: Click **Browse** to select the collection to which you want to deploy the Windows To Go package.  

    3.  **Use default distribution point groups associated to this collection**: Select this option if you want to store the package content on the collections default distribution point group. If you have not associated the selected collection with a distribution point group, this option will be unavailable.  

6.  On the **Content** page, click **Add** and then select the distribution points or distribution point groups to which you want to deploy the content associated with this package and program.  

7.  On the **Deployment Settings** page, select **Available** for the deployment type, and then click **Next**.  

8.  On the **Scheduling**, configure when this package and program will be deployed or made available to client devices.  

     The options on this page will differ depending on whether the deployment action is set to **Available** or **Required**.  

9. On the **Scheduling**, configure the following settings, and then click **Next**.  

    1.  **Schedule when this deployment will become available**: Specify the date and time when the package and program is available to run on the destination computer. When you select **UTC**, this setting ensures that the package and program is available for multiple destination computers at the same time rather than at different times, according to the local time on the destination computers.  

    2.  **Schedule when this deployment will expire**: Specify the date and time when the package and program expires on the destination computer. When you select **UTC**, this setting ensures that the task sequence expires on multiple destination computers at the same time rather than at different times, according to the local time on the destination computers.  

10. On the **User Experience** page of the Wizard, specify the following information:  

    -   **Software installation**: Allows the software to be installed outside of any configured maintenance windows.  

    -   **System restart (if required to complete the installation)**: Allows a device to restart outside of configured maintenance windows when required by the software installation.  

    -   **Embedded Devices**: When you deploy packages and programs to Windows Embedded devices that are write filter enabled, you can specify to install the packages and programs on the temporary overlay and commit changes later, or commit the changes at the installation deadline or during a maintenance window. When you commit changes at the installation deadline or during a maintenance window, a restart is required and the changes persist on the device.  

11. On the **Distribution Points** page, specify the following information:  

    -   **Deployment options:** Specify **Download content from distribution point and run locally**.  

    -   **Allow clients to share content with other clients on the same subnet**: Select this option to reduce load on the network by allowing clients to download content from other clients on the network that have already downloaded and cached the content. This option utilizes Windows BranchCache and can be used on computers running Windows Vista SP2 and later.  

    -   **All clients to use a fallback source location for content**: Specify whether to allow clients to fall back and use a non-preferred distribution point as the source location for content when the content is not available on a preferred distribution point.  

12. Complete the wizard.  

#### To deploy the Windows 8 task sequence  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  Select the Windows 8 task sequence that you created in the [Prerequisites to provision Windows To Go](#BKMK_Prereqs) step.  

4.  On the **Home** tab, in the **Deployment** group, click **Deploy**.  

5.  On the **General** page, specify the following settings:  

    1.  **Task sequence**: Verify that the Windows 8 task sequence is selected.  

    2.  **Collection**: Click **Browse** to select the collection that includes all devices for which a user might provision Windows To Go.  

        > [!IMPORTANT]  
        >  If the prestaged media that you created in the [Create prestaged media](#BKMK_CreatePrestagedMedia) section uses the SMSTSPreferredAdvertID variable, you can deploy the task sequence to the **All Systems** collection and specify the **Windows PE only (hidden)** setting on the **Content** page. Because the task sequence is hidden, it will only be available to media.  

    3.  **Use default distribution point groups associated to this collection**: Select this option if you want to store the package content on the collections default distribution point group. If you have not associated the selected collection with a distribution point group, this option will be unavailable.  

6.  On the **Deployment Settings** page, configured the following settings, and then click **Next**.  

    -   **Purpose**: Select **Available**. When you deploy the task sequence to a user, the user sees the published task sequence in the Application Catalog and can request it on demand. If you deploy the task sequence to a device, the user will see the task sequence in Software Center and can install it on demand.  

    -   **Make available to the following**: Specify whether the task sequence is available to Configuration Manager clients, media, or PXE.  

        > [!IMPORTANT]  
        >  Use the **Only media and PXE (hidden)** setting for automated task sequence deployments. Select **Allow unattended operating system deployment** and set the SMSTSPreferredAdvertID variable as part of the prestaged media to have the computer automatically boot to the Windows To Go deployment with no user interaction when it detects a Windows To Go drive. For more information about these prestaged media settings, see the [Create prestaged media](#BKMK_CreatePrestagedMedia) section.  

7.  On the **Scheduling** page, configure the following settings, and then click **Next**.  

    1.  **Schedule when this deployment will become available**: Specify the date and time when the task sequence is available to run on the destination computer. When you select **UTC**, this setting ensures that the task sequence is available for multiple destination computers at the same time rather than at different times, according to the local time on the destination computers.  

    2.  **Schedule when this deployment will expire**: Specify the date and time when the task sequence expires on the destination computer. When you select **UTC**, this setting ensures that the task sequence expires on multiple destination computers at the same time rather than at different times, according to the local time on the destination computers.  

8.  On the **User Experience** page, specify the following information:  

    -   **Show Task Sequence progress**: Specify whether the Configuration Manager client displays the progress of the task sequence.  

    -   **Software installation**: Specify whether the user is allowed to install software outside a configured maintenance windows after the scheduled time.  

    -   **System restart (if required to complete the installation)**: Allows a device to restart outside of configured maintenance windows when required by the software installation.  

    -   **Embedded Devices**: When you deploy packages and programs to Windows Embedded devices that are write filter enabled, you can specify to install the packages and programs on the temporary overlay and commit changes later, or commit the changes at the installation deadline or during a maintenance window. When you commit changes at the installation deadline or during a maintenance window, a restart is required and the changes persist on the device.  

    -   **Internet-based clients**: Specify whether the task sequence is allowed to run on an Internet-based client. Operations that install software, such as an operating system, are not supported with this setting. Use this option only for generic script-based task sequences that perform operations in the standard operating system.  

9. On the **Alerts** page, specify the alert settings that you want for this task sequence deployment, and then click **Next**.  

10. On the **Distribution Points** page, specify the following information, and then click **Next**.  

    -   **Deployment options**: Select **Download content locally when needed by running task sequence**.  

    -   **When no local distribution point is available, use a remote distribution point**: Specify whether clients can use distribution points that are on slow and unreliable networks to download the content that is required by the task sequence.  

    -   **Allow clients to use a fallback source location for content**:
        - *Prior to version 1610*, you can select the Allow fallback source location for content check box to allow clients outside these boundary groups to fall back and use the distribution point as a source location for content when no other distribution points are available.
        - *Beginning with version 1610*, you no longer can configure **Allow fallback source location for content**.  Instead, you configure relationships between boundary groups that determine when a client can begin to search additional boundary groups for a valid content source location. 

11. Complete the wizard.  

###  <a name="BKMK_UserExperience"></a> User runs the Windows To Go Creator  
 After you deploy the Windows To Go package and Windows 8 task sequence, the Windows To Go Creator is available to the user. The user can go to the software catalog, or Software Center if the Windows To Go Creator was deployed to devices, and run the Windows To Go Creator program. Once the creator package is downloaded, a flashing icon is displayed on the task bar. When the user clicks the icon, a dialog box is displayed for the user to select the Windows To Go drive to provision (unless the /drive command-line option is used). If the drive does not meet the requirements for Windows To Go or if the drive does not have enough free disk space to install the image, the creator program displays an error message. The user can verify the drive and image that will be applied from the confirmation page. As the creator configures and prestages content to the Windows To Go drive, it displays a progress dialog box. After the prestaging is complete, the creator displays a prompt to restart the computer to boot to the Windows To Go drive.  

> [!NOTE]  
>  If you did not enable boot redirection as part of the command line for the creator program in the [Create a Windows To Go Creator package](#BKMK_CreatePackage) section, the user might be required to manually boot to the Windows To Go drive on every system restart.  

###  <a name="BKMK_ConfigureStageDrive"></a> Configuration Manager configures and stages the Windows To Go drive  
 After the computer restarts to the Windows To Go drive, the drive will boot into Windows PE and connect to the management point to get the policy to complete the operating system deployment. Configuration Manager configures and stages the drive. After Configuration Manager stages the drive, the user can restart the computer to finalize the provisioning process (such as to join a domain or install apps). This process is the same for any prestaged media.  

###  <a name="BKMK_UserLogsIn"></a> User logs in to Windows 8  
 After Configuration Manager completes the provisioning process and the Windows 8 lock screen is displayed, the user can login to the operating system.  
