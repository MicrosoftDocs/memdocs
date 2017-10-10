---
title: Task sequence steps
titleSuffix: "Configuration Manager"
description: "Learn about the task sequence steps that you can add to a Configuration Manager task sequence."
ms.custom: na
ms.date: 03/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
caps.latest.revision: 26
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe

---
# Task sequence steps in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The following task sequence steps can be added to a Configuration Manager task sequence. For information about editing a task sequence, see [Edit a task sequence](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  


##  <a name="BKMK_ApplyDataImage"></a> Apply Data Image Task Sequence Step  
 Use the **Apply Data Image** task sequence step to copy the data image to the specified destination partition.  

 This step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Task sequence action variables](task-sequence-action-variables.md).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Image Package**  
 Specify the **Image Package** that will be used by this task sequence step by clicking **Browse**. Select the package you want to install in the **Select a Package** dialog box. The associated property information for each existing image package is displayed at the bottom of the **Select a Package** dialog box. Use the drop-down list to select the **Image** you want to install from the selected **Image Package**.  

> [!NOTE]  
>  This task sequence action treats the image as a data file and does not do any of the setup necessary to boot the image as an operating system.  

 **Destination**  
 Specifies an existing formatted partition and hard disk, specific logical drive letter, or the name of a task sequence variable that contains the logical drive letter.  

-   **Next available partition** - Use the next sequential partition that has not been previously targeted by an Apply Operating System or Apply Data Image action in this task sequence.  

-   **Specific disk and partition** - Select the **Disk** number (starting with 0) and the **Partition** number (starting with 1).  

-   **Specific logical drive letter** - Specify the **Drive Letter** assigned to the partition by Windows PE. Note that this drive letter can be different from the drive letter that the newly deployed operating system will assign.  

-   **Logical drive letter stored in a variable** - Specify the task sequence variable containing the drive letter assigned to the partition by Windows PE. This variable would typically be set in Advanced section of the **Partition Properties** dialog box for the **Format and Partition Disk** task sequence action.  

 **Delete all content on the partition before applying the image**  
 Specifies that all files on the target partition will be deleted before the image is installed. By not deleting the content of the partition, this step can be used to apply additional content to a previously targeted partition.  

##  <a name="BKMK_ApplyDriverPackage"></a> Apply Driver Package  
 Use the **Apply Driver Package** task sequence step to download all of the drivers in the driver package and install them on the Windows operating system.

 The **Apply Driver Package** task sequence step makes all device drivers in a driver package available for use by Windows. This step can be added to a task sequence between the **Apply Operating System**  and the **Setup Windows and ConfigMgr** steps to make the device drivers in the driver package available to Windows. Typically, the **Apply Driver Package** step is placed after the **Auto Apply Drivers** task sequence step. The **Apply Driver Package** task sequence step is also useful with stand-alone media deployment scenarios.  

 Ensure that similar device drivers are put into a driver package and distribute them to the appropriate distribution points. After they are distributed Configuration Manager client computers can install them. For example, you can put all the device drivers from a manufacturer into a driver package, and then distribute the package to distribution points where the associated computers can access them.

 This step is useful for stand-alone media and for administrators who want to install a specific set of drivers, including drivers for devices that would not be detected in a Plug-n-Play scan (for example, network printers).  

 This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Apply Driver Package Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Driver package**  
 Specify the driver package that contains the needed device drivers by clicking **Browse** and launching the **Select a Package** dialog box. Specify an existing package to be made available. The associated package properties are displayed at the bottom of the dialog box.  

 **Select the mass storage driver within the package that needs to be installed before setup on pre-Windows Vista operating systems**  
 Specify any mass storage device drivers that are needed for pre- Windows Vista operating system installations.  

 **Driver**  
 Select the mass storage device driver file to be installed before setup on pre-Windows Vista operating system deployments. The drop-down list is populated from the specified package.  

 **Model**  
 Specify the boot-critical device that is needed for pre-Windows Vista operating system deployments.  

 **Do unattended installation of unsigned drivers on version of Windows where this is allowed**  
 Select this option to allow Windows to install drivers that are unsigned on the reference computer.  

##  <a name="BKMK_ApplyNetworkSettings"></a> Apply Network Settings Step  
 Use the **Apply Network Settings** task sequence step to specify the network or workgroup configuration information for the destination computer. The specified values are stored in the appropriate answer file format for use by Windows Setup when the **Setup Windows and ConfigMgr** task sequence step is run.  

 This task sequence step runs in either a standard operating system or Windows PE. For more information about the task sequence variables for this action, see [Apply Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Join a workgroup**  
 Select this option to have the destination computer join the specified workgroup. Enter the name of the workgroup on the **Workgroup** line. This value can be overridden by the value that is captured by the **Capture Network Settings** task sequence step.  

 **Join a domain**  
 Select this option to have the destination computer join the specified domain. Specify or browse to the domain, such as *fabricam.com*. Specify or browse to a Lightweight Directory Access Protocol (LDAP) path for an organizational unit (i.e. LDAP//OU=computers, DC=Fabricam.com, C=com).  

 **Account**  
 Click **Set** to specify an account with the necessary permissions to join the computer to the domain. In the **Windows User Account** dialog box you can enter the user name using the following format: **Domain\User** .  

 **Adapter settings**  
 Specify network configurations for each network adapter in the computer. Click **New** to open the **Network Settings** dialog box, and then specify the network settings. If network settings were captured in a previous **Capture Network Settings** task sequence step, the previous settings are applied to the network adapter and the settings specified in this in this step are not applied. If network settings were not previously captured, the settings specified in the **Apply Network Settings** step are applied to network adapters in Windows device enumeration order.  

##  <a name="BKMK_ApplyOperatingSystemImage"></a> Apply Operating System Image  
 Use the **Apply Operating System Image** task sequence step to install an operating system on the destination computer. This task sequence step performs a set of actions depending on whether it is using an operating system image or an operating system installation package to install the operating system.  

 The **Apply Operating System Image** step performs the following actions when an operating system image is used.  

1.  Deletes all content on the targeted volume except for those files under the folder specified by the &#95;SMSTSUserStatePath task sequence variable.  

2.  Extracts the contents of the specified .wim file to the specified destination partition.  

3.  Prepares the answer file:  

    1.  Creates a new default Windows Setup answer file (sysprep.inf or unattend.xml) for the operating system that is being deployed.  

    2.  Merges any values from the user-supplied answer file.  

4.  Copies Windows boot loaders into the active partition.  

5.  Sets up the boot.ini or the Boot Configuration Database (BCD) to reference the newly installed operating system.  

 The **Apply Operating System Image** step performs the following actions when an operating system installation package is used.  

1.  Deletes all content on the targeted volume except for those files under the folder specified by the &#95;SMSTSUserStatePath task sequence variable.  

2.  Prepares the answer file:  

    1.  Creates a fresh answer file with standard values created by Configuration Manager.  

    2.  Merges any values from the user-supplied answer file.  

> [!NOTE]  
>  Actual installation of Windows is started by the **Setup Windows and ConfigMgr** task sequence step. After the **Apply Operating System** task sequence action has run, the OSDTargetSystemDrive task sequence variable is set to the drive letter of the partition containing the operating system files.  

 This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Apply Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   **Access content directly from the distribution point**:  

     Use this option to specify whether you want the task sequence to access the operating system image directly from the distribution point. For example, you can use this option when you deploy operating systems to embedded devices that have limited storage capacity. When this option is selected, you must also configure the package share settings on the **Data Access** tab of the package properties.  

    > [!NOTE]  
    >  This setting overrides the deployment option that is configured on the **Distribution Points** page in the **Deploy Software Wizard** only for the operating system image specified in this task sequence step, and not all content for the entire task sequence.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Apply operating system from a captured image**  
 Installs an operating system image that has previously been captured. Click **Browse** to open the **Select a package** dialog box, and then select the existing image package you want to install. If multiple images are associated with the specified **Image package**, use the drop-down list to specify the associated image that will be used for this deployment. You can view basic information about each existing image by clicking on the image.  

 **Apply operating system image from an original installation source**  
 Installs an operating system using an original installation source. Click **Browse** to open the **Select and Operating System Install Package** dialog box, and then select the existing operating system installation package you want to use. You can view basic information about each existing image source by clicking on the image source. The associated image source properties are displayed in the results pane at the bottom of the dialog box. If there are multiple editions associated with the specified package, use the drop-down list to specify the associated **Edition** that is used.  

 **Use an unattended or sysprep answer file for a custom installation**  
 Use this option to provide a Windows setup answer file (**unattend.xml**, **unattend.txt**, or **sysprep.inf**) depending on the operating system version and installation method. The file you specify can include any of the standard configuration options supported by Windows answer files. For example, you can use it to specify the default Internet Explorer home page. You must specify the package that contains the answer file and the associated path to the file in the package.  

> [!NOTE]  
>  The Windows setup answer file that you supply can contain embedded task sequence variables of the form %*varname*%, where varname is the name of the variable. The %*varname*% string will be substituted for the actual variable values in the **Setup Windows and ConfigMgr** task sequence action. Note however, that such embedded task sequence variables cannot be used in numeric-only fields in an unattend.xml answer file.  

 If you do not supply a Windows setup answer file, this task sequence action will automatically generate an answer file.  

 **Destination**  
 Specifies an existing formatted partition and hard disk, specific logical drive letter, or the name of a task sequence variable that contains the logical drive letter.  

-   **Next available partition** - Use the next sequential partition that has not been previously targeted by an Apply Operating System or Apply Data Image action in this task sequence.  

-   **Specific disk and partition** - Select the **Disk** number (starting with 0) and the **Partition** number (starting with 1).  

-   **Specific logical drive letter** - Specify the **Drive Letter** assigned to the partition by Windows PE. Note that this drive letter can be different from the drive letter that the newly deployed operating system will assign.  

-   **Logical drive letter stored in a variable** - Specify the task sequence variable containing the drive letter assigned to the partition by Windows PE. This variable would typically be set in Advanced section of the **Partition Properties** dialog box for the **Format and Partition Disk** task sequence action.  

##  <a name="BKMK_ApplyWindowsSettings"></a> Apply Windows Settings  
 Use the **Apply Windows Settings** task sequence step to configure the Windows settings for the destination computer. The specified values are stored in the appropriate answer file format for use by Windows Setup when the **Setup Windows and ConfigMgr** task sequence step is run.  

 This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Apply Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step  

 **Description**  
 More detailed information about the action taken in this step.  

 **User name**  
 Specify the registered user name that is associated with the destination computer. This value can be overridden by the value that is captured by the **Capture Windows Settings** task sequence action.  

 **Organization name**  
 Specify the registered organization name that is associated with the destination computer. This value can be overridden by the value that is captured by the **Capture Windows Settings** task sequence action.  

 **Product key**  
 Specify the product key that is used for the Windows installation on the destination computer.  

 **Server licensing**  
 Specify the server licensing mode. You can select **Per server** or **Per user** as the licensing mode. If you select per Server as the licensing mode you will also need to specify the maximum number of connections that will be permitted per your license agreement. Select **Do not specify** if the destination computer is not a server or you do not want to specify the licensing mode.  

 **Maximum connections**  
 Specify the maximum number of connections that are available for this computer as stated in your license agreement.  

 **Randomly generate the local administrator password and disable the account on all supported platforms (recommended)**  
 Select this option to randomly generate a local administrator password. This creates a local administrator password and causes the account to be disabled on supported platforms.  

 **Enable the account and specify the local administrator password**  
 Select this option to enable the local administrator account and create the local administrator password. Enter the password on the **Password** line and confirm the password on the **Confirm password** line.  

 **Time Zone**  
 Specify the time zone to configure on the destination computer. This value can be overridden by the value that is captured by the **Capture Windows Settings** task sequence step.  

##  <a name="BKMK_AutoApplyDrivers"></a> Auto Apply Drivers  
 Use the **Auto Apply Drivers** task sequence step to match and install drivers as part of the operating system deployment.  

 The **Auto Apply Drivers** task sequence step performs the following actions:  

1.  Scans the hardware and finds the Plug-n-Play IDs for all devices present on the system.  

2.  Sends the list of devices and their Plug-n-Play IDs to the management point. The management point returns a list of compatible drivers from the driver catalog for each device. The management point considers all drivers regardless of what driver package they might be in. Only those drivers tagged with the specified driver category and those drivers that are not marked as disabled are considered.  

3.  For each device, the client picks the best driver that is appropriate for the operating system on which it is being deployed and that is on an accessible distribution point.  

4.  The selected driver or drivers are downloaded from a distribution point and staged on the target operating system.  

    1.  For image-based installations, the drivers are placed into the operating system driver store.  

    2.  For setup-based installations, Windows Setup is configured with where to find the drivers.  

5.  When the **Setup Windows and ConfigMgr** task sequence action runs and Windows initially boots, it will find the drivers staged by this action.  

> [!IMPORTANT]
>  The **Auto Apply Drivers** task sequence step cannot be used with stand-alone media because Windows Setup will have no connection to the Configuration Manager site.

This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Auto Apply Drivers Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Install only the best matched compatible drivers**  
 Specifies that the task sequence step installs only the best matched driver for each hardware device detected.  

 **Install all compatible drivers**  
 Specifies that the task sequence step installs all compatible drivers for each hardware device detected and allows Windows setup to choose the best driver. This option takes more network bandwidth and disk space because it downloads more drivers, but it can result in a better driver being selected.  

 **Consider drivers from all categories**  
 Specifies that the task sequence action searches all available driver categories for the appropriate device drivers.  

 **Limit driver matching to only consider drivers in selected categories**  
 Specifies that the task sequence action searches for device drivers in specified driver categories for the appropriate device drivers.  

 **Do unattended installation of unsigned drivers on versions of Windows where this is allowed**  
 Allows this task sequence action to install unsigned Windows device drivers.  

> [!IMPORTANT]  
>  This option does not apply to operating systems where driver signing policy cannot be configured.  

##  <a name="BKMK_CaptureNetworkSettings"></a> Capture Network Settings  
 Use the **Capture Network Settings** task sequence step to capture Microsoft network settings from the computer running the task sequence. The settings are saved in task sequence variables that will override the default settings you configure on the **Apply Network Settings** task sequence step.  

 This task sequence step runs only in a standard operating system. It does not run in Windows PE. For more information about the task sequence variables for this action, see [Capture Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 Specifies a short user-defined name that describes the action taken in this step.  

 **Description**  
 Provides more detailed information about the action taken in this step.  

 **Migrate domain and workgroup membership**  
 Captures the domain and workgroup membership information of the destination computer.  

 **Migrate network adapter configuration**  
 Captures the network adapter configuration of the destination computer. The captured information includes the global network settings, the number of adapters, and the network settings associated with each adapter. These settings include settings associated with DNS, WINS, IP, and port filters.  

##  <a name="BKMK_CaptureOperatingSystemImage"></a> Capture Operating System Image  
 Use the **Capture Operating System Image** task sequence step to capture one or more images from a reference computer and store them in a WIM file on the specified network share. The Add Operating System Image Package Wizard can then be used to import this .WIM file into Configuration Manager so that it can be used for image-based operating system deployments.  

 Each volume (drive) on the reference computer is captured as a separate image within the .wim file. If the referenced computer has multiple volumes, the resulting WIM file will contain a separate image for each volume. Only volumes that are formatted as NTFS or FAT32 are captured. Volumes with other formats and USB volumes are skipped.  

 The installed operating system on the reference computer must be a version of Windows that is supported by Configuration Manager and must have been prepared by using the SysPrep tool. The installed operating system volume and the boot volume must be the same volume.  

 You must also enter a Windows account that has write permissions to the network share that you selected.  

 This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Capture Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Target**  
 File system pathname to the location that Configuration Manager uses when storing the captured operating system image.  

 **Description**  
 An optional user-defined description of the captured operating system image that is stored in the .WIM file.  

 **Version**  
 An optional user-defined version number to assign to the captured operating system image. This value can be any combination of letters and numbers and is stored in the .WIM file.  

 **Created by**  
 The optional name of the user that created the operating system image and is stored in the WIM file.  

 **Capture operating system image account**  
 You must enter the Windows account that has permissions to the network share you specified. Click **Set** to specify the name of that Windows account.  

##  <a name="BKMK_CaptureUserState"></a> Capture User State  
 Use the **Capture User State** task sequence step to use the User State Migration Tool (USMT) to capture user state and settings from the computer running the task sequence. This task sequence step is used in conjunction with the **Restore User State** task sequence step. With USMT 3.0.1 and later, this option always encrypts the USMT state store by using an encryption key generated and managed by Configuration Manager.  

 For more information about managing the user state when deploying operating systems, see [Manage user state](../get-started/manage-user-state.md).  

 You can also use the **Capture User State** task sequence step with the **Request State Store** and **Release State Store** task sequence steps if you want to save the state settings to or restore settings from a state migration point in the Configuration Manager site.  

 The **Capture User State** task sequence step provides control over a limited subset of the most commonly used USMT options. Additional command-line options can be specified using the OSDMigrateAdditionalCaptureOptions task sequence variable.  

 This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Capture User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureUserState).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **User state migration tool package**  
 Enter the Configuration Manager package that contains the version of USMT for this task sequence step to use when capturing the user state and settings. This package does not require a program. When the task sequence step is run, the task sequence will use the version of USMT in the package you specify. Specify a package containing the 32-bit or x64 version of USMT depending upon the architecture of the operating system from which you are capturing the state.  

 **Capture all user profiles with standard options**  
 Select this option to migrate all user profile information. This option is selected by default.  

 If you select this option, but do not select the option to Restore local computer user profiles in the Restore User State task sequence step, the task sequence will fail because Configuration Manager cannot migrate the new accounts without assigning them passwords. Also, if you use the **New Task Sequence** wizard and create a task sequence to **Install an existing image package**, the resulting task sequence defaults to Capture all user profiles with standard options, but does not select the option to Restore local computer user profiles (i.e. non-domain accounts).  

 Select **Restore local computer user profiles** and provide a password for the account to be migrated. In a manually created task sequence, this setting is found under the Restore User State step. In a task sequence created by the **New Task Sequence** wizard, this setting is found under the step **Restore User Files and Settings** wizard page.  

 If you have no local user accounts, this does not apply.  

 **Customize how user profiles are captured**  
 Select this option to specify a custom profile file migration. Click **Files** to select the configuration files for USMT to use with this step. You must specify a custom .xml file that contains rules that define the user state files to migrate.  

 **Click here to select configuration files:**  
 Select this option to select the configuration files in the USMT package you want to use for capturing user profiles. Click the **Files** button to launch the **Configuration Files** dialog box. To specify a configuration file, enter the name of the file on the **Filename** line and click the **Add** button.  

 **Enable verbose logging**  
 Enable this option to generate more detailed log file information. When capturing state, the log Scanstate.log is generated and stored in the task sequence Log folder in the \windows\system32\ccm\logs folder by default.  

 **Skip files using encrypted file system**  
 Enable this option if you want to skip capturing files that are encrypted with the Encrypted File System (EFS), including profile files. Depending on the operating system and the USMT version, encrypted files might not be readable after you restore. For more information, see the USMT documentation.  

 **Copy by using file system access**  
 Enable this option to specify any of the following settings:  

-   **Continue if some files cannot be captured**: Enable this setting to continue the migration process even if some files cannot be captured. If you disable this option, if a file cannot be captured then the task sequence step will fail. This option is enabled by default.  

-   **Capture locally by using links instead of by copying files**: Enable this setting to use NTFS hard-links to capture files.  

     For more information about migrating data using hard-links, see [Hard-Link Migration Store](http://go.microsoft.com/fwlink/p/?LinkId=240222)  

-   **Capture in off-line mode (Windows PE only)**: Enable this setting to capture the user state while in Windows PE instead of the full operating system.  

 **Capture by using Volume Copy Shadow Services (VSS)**  
 This option allows you to capture files even if they are locked for editing by another application.  

##  <a name="BKMK_CaptureWindowsSettings"></a> Capture Windows Settings  
 Use the **Capture Windows Settings** task sequence step to capture the Windows settings from the computer running the task sequence. The settings are saved in task sequence variables that will override the default settings you configure on the **Apply Windows Settings** task sequence step.  

 This task sequence step runs in either Windows PE or a standard operating system. For more information about the task sequence variables for this action, see [Capture Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Migrate computer name**  
 Select this option to capture the NetBIOS computer name of the computer.  

 **Migrate registered user and organization names**  
 Select this option to capture the registered user and organization names from the computer.  

 **Migrate time zone**  
 Select this option to capture the time zone setting on the computer.  

##  <a name="BKMK_CheckReadiness"></a> Check Readiness  
 Use the **Check Readiness** task sequence step to verify that the target computer meets the specified deployment prerequisite conditions.  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step. For this step, do not select this setting or the step will only log the readiness checks and not stop the task sequence when a check fails.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Ensure minimum memory (MB)**  
 Select this setting to verify the amount of memory, in megabytes, installed on the target computer meets or exceeds the amount specified. By default, this setting is selected.  

 **Ensure minimum processor speed (MHz)**  
 Select this setting to verify that the speed of the processor, in megahertz (MHz), installed in the target computer meets or exceeds the amount specified. By default, this setting is selected.  

 **Ensure minimum free disk space (MB)**  
 Select this setting to verify that the amount of free disk space, in megabytes, on the target computer meets or exceeds the amount specified.  

 **Ensure current OS to be refreshed is**  
 Select this setting to verify that the operating system installed on the target computer meets the requirement that you specify. By default, this setting is selected with a value of **CLIENT**.  

##  <a name="BKMK_ConnectToNetworkFolder"></a> Connect To Network Folder  
 Use the **Connect to Network Folder** task sequence action to create a connection to a shared network folder.  

 This task sequence step runs in a standard operating system or Windows PE. For more information about the task sequence variables for this action, see [Connect to Network Folder Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

##  <a name="BKMK_DisableBitLocker"></a> Disable BitLocker  
 Use the **Disable BitLocker** task sequence step to disable the BitLocker encryption on the current operating system drive, or on a specific drive. This action leaves the key protectors visible in clear text on the hard drive, but it does not decrypt the contents of the drive. Consequently this action is completed almost instantly.  

> [!NOTE]  
>  BitLocker drive encryption provides low-level encryption of the contents of a disk volume.  

 If you have multiple drives encrypted, you must disable BitLocker on any data drives before disabling BitLocker on the operating system drive.  

 This step runs only in a standard operating system. It does not run in Windows PE.  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 Specifies a short user-defined name that describes the action taken in this step.  

 **Description**  
 Provides more detailed information about the action taken in this step.  

 **Current operating system drive**  
 Disables BitLocker on the current operating system drive.  

 **Specific drive**  
 Disables BitLocker on a specific drive. Use the drop-down list to specify the drive where BitLocker is disabled.  

##  <a name="BKMK_DownloadPackageContent"></a> Download Package Content  
 Use the **Download Package Content** task sequence step to download any of the following package types:  

-   Operating system images  

-   Operating system upgrade packages  

-   Driver packages  

-   Packages  

 This step works well in a task sequence to upgrade an operating system in the following scenarios:  

-   To use a single upgrade task sequence that can work with both x86 and x64 platforms. To do  this, include two **Download Package Content** steps in the **Prepare for Upgrade** group with conditions to detect the client architecture and download only the appropriate operating system upgrade package. Configure each **Download Package Content** step to use the same variable, and use the variable for the media path on the **Upgrade Operating System** step.  

-   To dynamically download an applicable driver package, use two **Download Package Content** steps with conditions to detect the appropriate hardware type for each driver package. Configure each **Download Package Content** step to use the same variable, and use the variable for the **Staged content** value in drivers section on the **Upgrade Operating System** step.  

> [!NOTE]    
> When you deploy a task sequence that contains the Download Package Content step, do not select **Download all content locally before starting the task sequence** for **Deployment options** on the **Distribution Points** page of the Deploy Software Wizard.  

This step runs in either a standard operating system or Windows PE. However, the option to save the package in the Configuration Manager client cache is not supported in WinPE.

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 Specifies a short user-defined name that describes the action taken in this step.  

 **Description**  
 Provides more detailed information about the action taken in this step.  

 **Select package** icon  
 Click the icon to select the package to download. After you select a package, you can click the icon again to choose another package.  

 **Place into the following location**  
 Choose to save the package in  one of the following locations:  

 -   **Task sequence working directory**  

 -   **Configuration Manager client cache**: You use this option to store the content in the clients cache. This allows the client to act as a peer cache source for other peer cache clients. For more information, see [Prepare Windows PE peer cache to reduce WAN traffic](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

 -   **Custom path**  

 **Save path as a variable**  
 You can save the path as a variable that you can  use in another task sequence step. Configuration Manager adds a numerical suffix to the variable name. For example, if you specify a variable of %*mycontent*% as a custom variable, it is the root for where all the referenced content is stored (which can be multiple packages). When you refer to the variable, you will add a numerical suffix to the variable. For example, for the first package, you will refer to %*mycontent01*% variable. When you refer to the variable in a subsequence steps, such as Upgrade Operating System, you would use %*mycontent02*% or %*mycontent03*% where the number corresponds to the order in which the package is listed in the step.  

 **If a package download fails, continue downloading other packages in the list**  
 Specifies that if the package download fails that it will go to the next package in the list and start the download.  

##  <a name="BKMK_EnableBitLocker"></a> Enable BitLocker  
 Use the **Enable BitLocker** task sequence step to enable BitLocker encryption on at least two partitions on the hard drive. The first active partition contains the Windows bootstrap code. Another partition contains the operating system. The bootstrap partition must remain unencrypted.  

 Use the **Pre-provision BitLocker** task sequence step to enable BitLocker on a drive while in Windows PE. For more information, see the [Pre-provision BitLocker](#BKMK_PreProvisionBitLocker) section in this topic.  

> [!NOTE]  
>  BitLocker drive encryption provides low-level encryption of the contents of a disk volume.  

 The **Enable BitLocker** step runs only in a standard operating system. It does not run in Windows PE. For more information about the task sequence variables for this action, see [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

 The Trusted Platform Module (TPM) must be in the following state when you specify **TPM Only**, **TPM and Startup Key on USB** or **TPM and PIN**, before you can run the **Enable BitLocker** step:  

-   Enabled  

-   Activated  

-   Ownership Allowed  

 The task sequence step can complete any remaining TPM initialization, because the remaining steps do not require physical presence or reboots. The remaining TPM initialization steps which can be completed transparently by **Enable BitLocker** (if necessary) include:  

-   Create endorsement key pair  

-   Create owner authorization value and escrow to Active Directory, which must have been extended to support this value  

-   Take ownership  

-   Create the storage root key, or reset if already present but incompatible  

 If you want the **Enable BitLocker** step to wait until the drive encryption process has been completed before continuing with the next step in the task sequence, select the **Wait** check box. If you do not select the **Wait** check box, the drive encryption process will be performed in the background and task sequence execution will proceed immediately to the next step.  

 BitLocker can be used to encrypt multiple drives on a computer system (both operating system and data drives). To encrypt a data drive, the operating system must already be encrypted and the encryption process must be completed, because the key protectors for the data drives are stored on the operating system drive. As a result, if you encrypt the operating system drive and the data drive in the same process, the wait option must be selected for the step that enables BitLocker for the operating system drive.  

 If the hard drive is already encrypted but BitLocker is disabled then Enable BitLocker re-enables the key protector or protectors and will be completed almost instantly. Re-encryption of the hard drive is not necessary in this case.  

 For more information about the task sequence variables for this action, see [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 Specifies a descriptive name for this task sequence step.  

 **Description**  
 Allows you to optionally enter a description for this task sequence step.  

 **Choose the drive to encrypt**  
 Specifies the drive to encrypt. To encrypt the current operating system drive, select **Current operating system drive** and then configure one of the following options for key management:  

-   **TPM only**: Select this option to use only Trusted Platform Module (TPM).  

-   **Startup Key on USB only**: Select this option to use a startup key stored on a USB flash drive. When you select this option, BitLocker locks the normal boot process until a USB device that contains a BitLocker startup key is attached to the computer.  

-   **TPM and Startup Key on USB**: Select this option to use TPM and a startup key stored on a USB flash drive. When you select this option, BitLocker locks the normal boot process until a USB device that contains a BitLocker startup key is attached to the computer.  

-   **TPM and PIN**:  Select this option to use TPM and a personal identification number (PIN). When you select this option, BitLocker locks the normal boot process until the user provides the PIN.  

 To encrypt a specific, non-operating system data drive, select **Specific drive**, and then select the drive from the list.  

 **Chose where to create the recovery key**  
 To specify where the recovery password is created, select **In Active Directory** to escrow the password in Active Directory. If you select this option you must extend Active Directory for the site so that the associated BitLocker recovery information is saved. You can decide to not create a password at all by selecting **Do not create recovery key**. However, creating a password is a best practice.  

 **Wait for BitLocker to complete the drive encryption process on all drives before continuing task sequence execution**  
 Select this option to allow the BitLocker drive encryption to be completed prior to running the next step in the task sequence. If this option is selected the entire disk volume will be encrypted before the user is able to log in to the computer.  

 The encryption process can take hours to be completed when a large hard drive is being encrypted. Not selecting this option will allow the task sequence to proceed immediately.  

##  <a name="BKMK_FormatandPartitionDisk"></a> Format and Partition Disk  
 Use the **Format and Partition Disk** task sequence step to format and partition a specified disk on the destination computer.  

> [!IMPORTANT]  
>  Every setting you specify for this task sequence step applies to a single specified disk. If you want to format and partition another disk on the destination computer, you must add an additional **Format and Partition Disk** task sequence step to the task sequence.  

 This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Format and Partition Disk Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Disk Number**  
 The physical disk number of the disk that will be formatted. The number is based on Windows disk enumeration ordering.  

 **Disk Type**  
 The type of the disk that is formatted. There are two options to select from the drop-down list:  

-   Standard(MBR) - Master Boot Record.  

-   GPT - GUID Partition Table  

> [!NOTE]  
>  If you change the disk type from **Standard (MBR)** to **GPT**, and the partition layout contains an extended partition, all extended and logical partitions will be removed from the layout. You will be prompted to confirm this action before changing the disk type.  

 **Volume**  
 Specific information about the partition or volume that will be created, including the following:  

-   Name  

-   Remaining disk space  

 To create a new partition, click **New** to launch the **Partition Properties** dialog box. You can specify the partition type and size, and specify if this will be a boot partition. To modify an existing partition, click the partition to be modified and then click the properties button. For more information about how to configure hard drive partitions, see one of the following:  

-   [How to Configure UEFI/GPT-Based Hard Drive Partitions](http://go.microsoft.com/fwlink/?LinkID=272104)  

-   [How to Configure BIOS/MBR-Based Hard Drive Partitions](http://go.microsoft.com/fwlink/?LinkId=272105)  

 To delete a partition, select the partition to be deleted and then click **Delete**.  

##  <a name="BKMK_InstallApplication"></a> Install Application  
 Use the **Install Application** task sequence step to install applications as part of the task sequence. This step can install a set of applications that are specified by the task sequence step or a set of applications that are specified by a dynamic list of task sequence variables. When this step is run, the application installation begins immediately without waiting for a policy polling interval.  

 The applications that are installed must meet the following criteria:  

-   The application must be a deployment type of Windows Installer or Script installer. Windows app package (.appx file) deployment types are not supported.  

-   It must run under the local system account and not the user account.  

-   It must not interact with the desktop. The program must run silently or in an unattended mode.  

-   It must not initiate a restart on its own. The application must request a restart by using the standard restart code, a 3010 exit code. This ensures that the task sequence step will handle the restart correctly. If the application does return a 3010 exit code, the underlying task sequence engine performs the restart. After the restart, the task sequence automatically continues.  

 When the **Install Application** step runs, the application checks the applicability of the requirement rules and detection method on the deployment types of the application. Based on the results of this check, the application installs the applicable deployment type. If a deployment type contains dependencies, the dependent deployment type is evaluated and installed as part of the install application step. Application dependencies are not supported for stand-alone media.  

> [!NOTE]  
>  To install an application that supersedes another application, the content files for the superseded application must be available or the task sequence step will fail. For example, Microsoft Visio 2010 is installed on a client or in a captured image. When the Install Application task sequence step is run to install Microsoft Visio 2013, the content files for Microsoft Visio 2010 (the superseded application) must be available on a distribution point or the task sequence will fail. A client or captured image without Microsoft Visio installed will complete the Microsoft Visio 2013 installation without checking for the Microsoft Visio 2010 content files.  

> [!NOTE]
> You can use the SMSTSMPListRequestTimeoutEnabled and SMSTSMPListRequestTimeout built-in variables to enable and specify how many milliseconds a task sequence waits before it retries to install an application or software update after it fails to retrieve the management point list from location services. For more information, see [Task sequence built-in varliables](task-sequence-built-in-variables.md).

 This task sequence step runs only in a standard operating system. It does not run in Windows PE.  

### Details  
 On the **Properties** tab for this step, you can configure the settings that are described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify to retry this step if the computer unexpectedly restarts. You can also specify how many times to retry after a restart.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Install the following applications**  
 This setting specifies the applications that are installed in the order that they are specified.  

 Configuration Manager will filter out any disabled applications or any applications with the following settings. These applications will not appear in the **Select the application to install** dialog box.  

-   Only when a user is logged on  

-   Run with user rights  

 **Install applications according to dynamic variable list**  
 This setting specifies the base name for a set of task sequence variables that are defined for a collection or for a computer. These variables specify the applications that will be installed for that collection or computer. Each variable name consists of its common base name plus a numerical suffix starting at 01. The value for each variable must contain the name of the application and nothing else.  

 For applications to be installed by using a dynamic variable list, the following setting must be enabled on the **General** tab of the application's **Properties** dialog box: **Allow this application to be installed from the Install Application task sequence action instead of deploying manually**  

> [!NOTE]  
>  You cannot install applications by using a dynamic variable list for stand-alone media deployments.  

 For example, to install a single application by using a task sequence variable called AA01, you specify the following variable:  

|Variable Name|Variable Value|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

 To install two applications, you would specify the following variables:  

|Variable Name|Variable Value|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

 The following conditions will affect what is installed:  

-   If the value of a variable contains any information other than the name of the application. That application is not installed and the task sequence continues.  

-   If no variable with the specified base name and "01" suffix are found, no applications are installed. When you select **Continue on error** on the Options tab of the task sequence step, the task sequence continues when an application fails to install. When the setting is not selected, the task sequence fails and will not install remaining applications.  

 **If an application fails, continue installing other applications in the list**  
 This setting specifies that the step continues if an individual application installation fails. If this setting is specified, the task sequence will continue regardless of any installation errors that are returned. If this is not specified an installation fails, the task sequence step will end immediately.  

##  <a name="BKMK_InstallPackage"></a> Install Package

 Use the **Install Package** task sequence step to install software as part of the task sequence. When this step is run, the installation begins immediately without waiting for a policy polling interval  

 The software that is installed must meet the following criteria:  

-   It must run under the local system account and not the user account.  

-   It should not interact with the desktop. The program must run silently or in an unattended mode.  

-   It must not initiate a restart on its own. The software must request a restart using the standard restart code, a 3010 exit code. This ensures that the task sequence step will properly handle the restart. If the software does return a 3010 exit code, the underlying task sequence engine will perform the restart. After the restart, the task sequence will automatically continue.  

 Programs that use the **Run another program first** option to install a dependent program are not supported when deploying an operating system. If **Run another program first** is enabled for the software and the dependent program has already been run on the destination computer, the dependent program will be run and the task sequence will continue. However, if the dependent program has not already been run on the destination computer, the task sequence step will fail.  

> [!NOTE]  
>  The central administration site does not have the necessary client configuration policies that are required to enable the software distribution agent during the execution of the task sequence. When you create stand-alone media for a task sequence at the central administration site, and the task sequence includes an **Install Package** step, the following error might appear in the CreateTsMedia.log file:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  For stand-alone media that includes an Install Package step, you must create the stand-alone media at a primary site that has the software distribution agent enabled or add a **Run Command Line** step after the **Setup Windows and ConfigMgr** step and before the first **Install Package** step. The **Run Command Line** step runs a WMIC command to enable the software distribution agent before the first Install package step runs. You can use the following in your **Run Command Line** task sequence step:  
>   
>  **Command Line**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  
>   
>  For more information about creating stand-alone media, see [Create stand-alone media](../deploy-use/create-stand-alone-media.md).  

 This task sequence step runs only in a standard operating system. It does not run in Windows PE.  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Install a single software package**  
 This setting specifies a Configuration Manager software package. The step will wait until the installation is complete.  

 **Install software packages according to dynamic variable list**  
 This setting specifies the base name for a set of task sequence variables that are defined for a collection or for a computer. These variables specify the packages that will be installed for that collection or computer. Each variable name consists of its common base name plus a numerical suffix starting at 001. The value for each variable must contain a package ID and the name of the software separated by a colon.  

 For software to be installed by using a dynamic variable list, the following setting must be enabled on the **Advanced** tab of the package's **Properties** dialog box: **Allow this program to be installed from the Install Package task sequence without being deployed**  

> [!NOTE]  
>  You cannot install software packages by using a dynamic variable list for stand-alone media deployments.  

 For example, to install a single software package by using a task sequence variable called AA001, you specify the following variable:  

|Variable Name|Variable Value|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

 To install three software packages, you would specify the following variables:  

|Variable Name|Variable Value|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

 The following conditions will affect what is installed:  

-   If the value of a variable is not created in the correct format or it does not specify a valid application ID and name, the installation of the software will fail.  

-   If the package Id contains lowercase characters, the installation of that software will fail.  

-   If no variables with the specified base name and "001" suffix are found, no packages are installed and the task sequence continues.  

 **If installation of a software package fails, continue installing other packages in the list**  
 This setting specifies that the step continues if an individual software package installation fails. If this setting is specified, the task sequence will continue regardless of any installation errors that are returned. If this is not specified an installation fails, the task sequence step will end immediately.  

##  <a name="BKMK_InstallSoftwareUpdates"></a> Install Software Updates  
 Use the **Install Software Updates** task sequence step to install software updates on the destination computer. The destination computer is not evaluated for applicable software updates until this task sequence step runs. At that time, the destination computer is evaluated for software updates like any other Configuration Manager-managed client. In particular, this step installs only the software updates that are targeted to collections of which the computer is currently a member.  
>  [!IMPORTANT]
>We highly recommend that you install the latest version of the Windows Update Agent for much better performance when using the Install Software Updates task sequence step.
>* For Windows 7, see [Knowledge base article 3161647](https://support.microsoft.com/kb/3161647).
>* For Windows 8, see [Knowledge base article 3163023](https://support.microsoft.com/kb/3163023).

 This task sequence step runs only in a standard operating system. It does not run in Windows PE. For information about task sequence variables for this task sequence action, see [Install Software Updates Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > You can use the SMSTSMPListRequestTimeoutEnabled and SMSTSMPListRequestTimeout built-in variables to enable and specify how many milliseconds a task sequence waits before it retries to install an application or software update after it fails to retrieve the management point list from location services. For more information, see [Task sequence built-in variables](task-sequence-built-in-variables.md).

> [!NOTE]
>On the options tab, you can configure this task sequence to retry if the computer unexpectedly restarts. For example, a software update installation that automatically restarts the computer. Beginning in Configuration Manager 1602, you can configure the SMSTSWaitForSecondReboot variable to  specify how long (in seconds) the task sequence should pause after the computer restarts when installing software updates. For more information, see [Task sequence built-in variables](task-sequence-built-in-variables.md).

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify to retry this step if the computer unexpectedly restarts. You can also specify how many times to retry after a restart.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Required for installation - Mandatory software updates only**  
 Select this option to install all software updates flagged in Configuration Manager as mandatory for the destination computers that receive the task sequence. Mandatory software updates have administrator-defined deadlines for installation.  

 **Available for installation - All software updates**  
 Select this option to install all available software updates targeting the Configuration Manager collection that will receive the task sequence. All available software updates will be installed on the destination computers.  

 **Evaluate software updates from cached scan results**  
Beginning in Configuration Manager version 1606, you have the option to do a full scan for software updates instead of using the cached scan results. By default, the task sequence uses cached results. You can clear the checkbox to have the client connect to the software update point to process and download the latest software updates catalog. You might chose this option when you use a task sequence to [capture and build an operating system image](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md), where you know there will be a large number of software updates, especially many that have dependencies (need to install X before Y will appear as applicable). When you clear this setting and deploy the task sequence to a large number of clients, they will all connect to the software update point at the same time. This might result in performance issues during the process and download of the catalog. In most cases, we recommend that you use the default setting.

A new task sequence variable, SMSTSSoftwareUpdateScanTimeout, was introduced in Configuration Manager version 1606 to give you the ability to control the timeout for the software updates scan during the Install software updates task sequence step. The default value is 30 minutes. For more information, see [Task sequence built-in variables](task-sequence-built-in-variables.md).


##  <a name="BKMK_JoinDomainorWorkgroup"></a> Join Domain or Workgroup  
 Use the **Join Domain or Workgroup** task sequence step to add the destination computer to a workgroup or domain.  

 This task sequence step runs only in a standard operating system. It does not run in Windows PE. For information about task sequence variables for this task sequence action, see [Join Domain or Workgroup Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Join a workgroup**  
 Select this option to have the destination computer join the specified workgroup. If the computer is currently a member of a domain, selecting this option will cause the computer to reboot.  

 **Join a domain**  
 Select this option to have the destination computer join the specified domain.  

 Optionally, enter or browse for an organizational unit (OU) in the specified domain for the computer to join. If the computer is currently a member of some other domain or a workgroup, this will cause the computer to reboot. If the computer is already a member of some other OU, Active Directory Domain Services does not allow you to change the OU and this setting is ignored.  

 **Enter the account which has permission to join the domain**  
 Click **Set** to enter an account and password that has permissions to join the domain. The account must be entered in the following format:  

 *Domain\account*  

## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Prepare ConfigMgr Client for Capture  
Use the **Prepare ConfigMgr Client for Capture** step to remove the Configuration Manager client or configure the client on the reference computer to prepare it for capture as part of the imaging process.

Starting in Configuration Manager version 1610, the Prepare ConfigMgr Client step completely removes the Configuration Manager client, instead of only removing key information. When the task sequence deploys the captured operating system image it will install a new Configuration Manager client each time.  

> [!Note]  
>  The client is only removed during the **Build and capture a reference operating system image** task sequence. Other capture methods, such as capture media or a custom task sequence, will not remove the client.

Prior to Configuration Manager version 1610, this step performs the following tasks:  

-   Removes the client configuration properties section from the smscfg.ini file in the Windows directory. These properties include client-specific information including the Configuration Manager GUID and other client identifiers.  

-   Deletes all SMS or Configuration Manager machine certificates.  

-   Deletes the Configuration Manager client cache.  

-   Clears the assigned site variable for the Configuration Manager client.  

-   Deletes all local Configuration Manager policy.  

-   Removes the trusted root key for the Configuration Manager client.  

 This task sequence step runs only in a standard operating system. It does not run in Windows PE.  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

##  <a name="BKMK_PrepareWindowsforCapture"></a> Prepare Windows for Capture  
 Use the **Prepare Windows for Capture** task sequence step to specify the Sysprep options to use when capturing an operating system image on the reference computer. This task sequence action runs Sysprep and then reboots the computer into Windows PE boot image specified for the task sequence. The reference computer must not be joined to a domain for this action to be completed successfully.  

 This task sequence step runs only in a standard operating system. It does not run in Windows PE. For information about task sequence variables for this task sequence action, see [Prepare Windows for Capture Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Automatically build mass storage driver list**  
 Select this option to have Sysprep automatically build a list of mass storage drivers from the reference computer. This option enables the Build Mass Storage Drivers option in the sysprep.inf file on the reference computer. For more information about this setting, refer to the Sysprep documentation.  

 **Do not reset activation flag**  
 Select this option to prevent Sysprep from resetting the product activation flag.  

##  <a name="BKMK_PreProvisionBitLocker"></a> Pre-provision BitLocker  
 Use the **Pre-provision BitLocker** task sequence step to enable BitLocker on a drive while in Windows PE. Only the used drive space is encrypted, and therefore, encryption times are much faster. You apply the key management options by using the [Enable BitLocker](#BKMK_EnableBitLocker) task sequence step after the operating system installs. This step runs only in Windows PE. It does not run in a standard operating system.  

> [!IMPORTANT]  
>  To pre-provision BitLocker, you must deploy a minimum operating system of Windows 7 and TPM must be supported and enabled on the computer.  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 Specify a short user-defined name that describes the action taken in this step.  

 **Description**  
 Specify detailed information about the action taken in this step.  

 **Apply BitLocker to the specified drive**  
 Specify the drive for which you want to enable BitLocker. Only the used space on the drive is encrypted.  

 **Skip this step for computers that do not have a TPM or when TPM is not enabled**  
 Select this option to skip the drive encryption when the computer hardware does not support TPM or when TPM is not enabled. For example, you can use this option when you deploy an operating system to a virtual machine.  

##  <a name="BKMK_ReleaseStateStore"></a> Release State Store  
 Use the **Release State Store** task sequence step to notify the state migration point that the capture or restore action is complete. This step is used in conjunction with the **Request State Store**, **Capture User State**, and **Restore User State** task sequence steps to migrate user state data using a state migration point and the User State Migration Tool (USMT).  

 For more information about managing the user state when deploying operating systems, see [Manage user state](../get-started/manage-user-state.md).  

 If you requested access to a state migration point to capture user state in the **Request State Store**  task sequence step, this step notifies the state migration point that the capture process is complete and that the user state data is available to be restored. The state migration point sets the access control permissions for the captured state so that it can only be accessed (as read-only) by the restoring computer.  

 If you requested access to a state migration point to restore user state in the **Request State Store** task sequence step, this task sequence step notifies the state migration point that the restore process is complete. At this point, whatever retention settings you configured for the state migration point are activated.  

> [!IMPORTANT]  
>  It is a best practice to set **Continue on Error** on any task sequence steps between the **Request State Store** step and **Release State Store** step so that every **Request State Store** task sequence action has a matching **Release State Store** task sequence action.  

 This task sequence step runs only in a standard operating system. It does not run in Windows PE. For information about task sequence variables for this task sequence action, see [Release State Store Sequence Action Variables](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

##  <a name="BKMK_RequestStateStore"></a> Request State Store  
 Use the **Request State Store** task sequence step to request access to a state migration point when capturing state from a computer or restoring state to a computer.  

 For more information about managing the user state when deploying operating systems, see [Manage user state](../get-started/manage-user-state.md).  

 You can use the **Request State Store** task sequence step in conjunction with the **Release State Store**, **Capture User State**, and **Restore User State** task sequence steps to migrate computer state using a state migration point and the User State Migration Tool (USMT).  

> [!NOTE]  
>  If you have just established a new state migration point site role (SMP), it can take up to one hour to be available for user state storage. To expedite the availability of the SMP you can adjust any state migration point property setting to trigger a site control file update.  

 This task sequence step runs in a standard operating system and in Windows PE for offline USMT. For information about the task sequence variables for this task sequence action, see [Request State Store Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RequestState).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Capture state from the computer**  
 Finds a state migration point that meets the minimum requirements as configured in the state migration point settings (maximum number of clients and minimum amount of free disk space) but it does not guarantee sufficient space is available at the time of state migration. Selecting this option will request access to the state migration point for the purpose of capturing the user state and settings from a computer.  

 If the Configuration Manager site has multiple state migration points enabled, this task sequence step finds a state migration point that has disk space available by querying the site's management point for a list of state migration points, and then evaluating each until it finds one that meets the minimum requirements.  

 **Restore state from another computer**  
 Select this option to request access to a state migration point for the purpose of restoring previously captured user state and settings to a destination computer.  

 If the Configuration Manager site has multiple state migration points, this task sequence step finds the state migration point that has the computer state that was stored for the destination computer.  

 **Number of retries**  
 The number of times that this task sequence step will try to find an appropriate state migration point before failing.  

 **Retry delay (in seconds)**  
 The amount of time in seconds that the task sequence step waits between retry attempts.  

 **If computer account fails to connect to a state store, use the network access account.**  
 Specifies that the Configuration Manager network access account credentials will be used to connect to the state migration point if the Configuration Manager client cannot access the SMP state store using the computer account. This option is less secure because other computers could use the network access account to access your stored state, but might be necessary if the destination computer is not domain joined.  

##  <a name="BKMK_RestartComputer"></a> Restart Computer  
 Use the **Restart Computer** task sequence step to restart the computer running the task sequence. After the restart, the computer will automatically continue with the next step in the task sequence.  

 This step can be run in either a standard operating system or Windows PE. For more information about the task sequence variables for this task sequence action, see [Restart computer task sequence action variables](task-sequence-action-variables.md#BKMK_RestartComputer).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **The boot image assigned to this task sequence**  
 Select this option for the destination computer to use the boot image that is assigned to the task sequence. The boot image will be used to run subsequent task sequence steps that run in Windows PE.  

 **The currently installed default operating system**  
 Select this option for the destination computer to reboot into the installed operating system.  

 **Notify the user before restarting**  
 Select this option to display a notification to the user that the destination computer will be restarted. This option is selected by default.  

 **Notification message**  
 Enter a notification message that is displayed to the user before the destination computer is restarted.  

 **Message display time-out**  
 Specify the amount of time in seconds that a user will be given before the destination computer is restarted. The default amount of time is sixty (60) seconds.  

##  <a name="BKMK_RestoreUserState"></a> Restore User State  
 Use the **Restore User State** task sequence step to initiate the User State Migration Tool (USMT) to restore user state and settings to the destination computer. This task sequence step is used in conjunction with the **Capture User State** task sequence step.  

 For more information about managing the user state when deploying operating systems, see [Manage user state](../get-started/manage-user-state.md).  

 You can also use the **Restore User State** task sequence step with the **Request State Store** and **Release State Store** task sequence steps if you want to save the state settings to or restore settings from a state migration point in the Configuration Manager site. With USMT 3.0 and above, this option always decrypts the USMT state store by using an encryption key generated and managed by Configuration Manager.  

 The **Restore User State** task sequence step provides control over a limited subset of the most commonly used USMT options. Additional command-line options can be specified by using the OSDMigrateAdditionalRestoreOptions task sequence variable.  

> [!IMPORTANT]  
>  If you are using the **Restore User State** task sequence step for a purpose unrelated to an operating system deployment scenario, add the [Restart Computer](#BKMK_RestartComputer) task sequence step immediately following the **Restore User State** task sequence step.  

 This task sequence step runs only in a standard operating system. It does not run in Windows PE. For information about the task sequence variables for this task sequence action, see [Restore User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RestoreUserState).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 Specifies a short user-defined name that describes the action taken in this step.  

 **Description**  
 Specifies more detailed information about the action taken in this step.  

 **User state migration tool package**  
 Enter the Configuration Manager package that contains the version of USMT for this step to use when restoring the user state and settings. This package does not require a program. When the task sequence step is run, the task sequence will use the version of USMT in the package you specify. Specify a package containing the 32-bit or x64 version of USMT depending upon the architecture of the operating system to which you are restoring the state.  

 **Restore all captured user profiles with standard options**  
 Restores the captured user profiles with the standard options. To customize the options that will be restored, select **Customize user profile capture**.  

 **Customize how user profiles are restored**  
 Allows you to customize the files that you want to restore to the destination computer. Click **Files** to specify the configuration files in the USMT package you want to use for restoring the user profiles. To add a configuration file, enter the name of the file in the **Filename** box, and then click **Add**. The configuration files that will be used for the operation are listed in the Files pane. The .xml file you specify defines which user file will be restored.  

 **Restore local computer user profiles**  
 Restores the local computer user (i.e. not domain user) profiles. You will need to assign new passwords to the restored local user accounts because the original local user account passwords cannot be migrated. Enter the new password in the **Password** box, and confirm the password in the **Confirm Password** box.  

 **Continue if some files cannot be restored**  
 Continues restoring user state and settings even if some files are unable to be restored. This option is enabled by default. If you disable this option and errors are encountered while restoring files, the task sequence step will end immediately with a failure and not all files will be restored.  

 **Enable verbose logging**  
 Enable this option to generate more detailed log file information. When restoring state, the log Loadstate.log is generated and stored in the task sequence log folder in the \windows\system32\ccm\logs folder by default.  

##  <a name="BKMK_RunCommandLine"></a> Run Command Line  
 Use the **Run Command Line** task sequence step to run a specified command line.  

 This step can be run in a standard operating system or Windows PE. For information about task sequence variables for this task sequence action, see [Run Command Line Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RunCommand).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 Specifies a short user-defined name that describes the command line that is run.  

 **Description**  
 Specifies more detailed information about the command line that is run.  

 **Command line**  
 Specifies the command line that is run. This field is required. Including file name extensions are a best practice, for example, .vbs and .exe. Include all required settings files, command-line options, or switches.  

 If the file name does not have a file name extension specified, Configuration Manager tries .com, .exe, and .bat. If the file name has an extension that is not an executable, Configuration Manager tries to apply a local association. For example, if the command line is readme.gif, Configuration Manager starts the application specified on the destination computer for opening .gif files.  

 Examples:  

 **setup.exe /a**  

 **cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat**  

> [!NOTE]  
>  Command-line actions, such as output redirection, piping, or copy, as in the preceding example, must be preceded by the **cmd.exe /c** command to run successfully.  

 **Disable 64-bit file system redirection**  
 By default, when running on a 64-bit operating system, the executable in the command line is located and run using the WOW64 file system redirector so that 32-bit versions of operating system executables and DLLs are found.  Selecting this option disables the use of the WOW64 file system redirector so that native 64-bit versions of operating system executables and DLLs can be found.  Selecting this option has no effect when running on a 32-bit operating system.  

 **Start in**  
 Specifies the executable folder for the program, up to 127 characters. This folder can be an absolute path on the destination computer or a path relative to the distribution point folder that contains the package. This field is optional.  

 Examples:  

 **c:\officexp**  

 **i386**  

> [!NOTE]  
>  The **Browse** button browses the local computer for files and folders, so anything you select this way must also exist on the destination computer in the same location and with the same file and folder names.  

 **Package**  
 When you specify files or programs on the command line that are not already present on the destination computer, select this option to specify the Configuration Manager package that contains the appropriate files. The package does not require a program. This option is not required if the specified files exist on the destination computer.  

 **Time-out**  
 Specifies a value that represents how long Configuration Manager will allow the command line to run. This value can be from 1 minute to 999 minutes. The default value is 15 minutes.  

 This option is disabled by default.  

> [!IMPORTANT]  
>  If you enter a value that does not allow enough time for the Run Command Line task sequence step to complete successfully, the task sequence step will fail and the entire task sequence could fail depending on other control settings. If the time-out expires, Configuration Manager will terminate the command-line process.  

 **Run this step as the following account**  
 Specifies that the command line is run as a Windows user account other than the local system account.  

> [!NOTE]  
>  When you specify another account for this step and it occurs after an operating system installation step, the account must be added to the computer before you can run simple scripts or commands and the profile for the Windows user account must be restored to run more complex programs, such as an MSI.  

 **Account**  
 Specifies the Run As Windows user account for the command-line task in the task sequence to be run by this action. The command line will be run with the permissions of the specified account. Click **Set** to specify the local user or domain account.  

> [!IMPORTANT]  
>  If a **Run Command Line** task sequence action specifying a user account is executed while in Windows PE, the action will fail because Windows PE cannot be joined to a domain. The failure will be recorded in the smsts.log file.  

##  <a name="BKMK_RunPowerShellScript"></a> Run PowerShell Script  
 Use the **Run PowerShell Script** task sequence step to run a specified PowerShell script.  

 This step can be run in a standard operating system or Windows PE. To run this step in Windows PE, PowerShell must be enabled in the boot image. You can enable Windows PowerShell (WinPE-PowerShell) from the **Optional Components** tab in the properties for the boot image. For more information about how to modify a boot image, see [Manage boot images](../get-started/manage-boot-images.md).  

> [!NOTE]  
>  PowerShell is not enabled by default on Windows Embedded operating systems.  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 Specifies a short user-defined name that describes the command line that is run.  

 **Description**  
 Specifies more detailed information about the command line that is run.  

 **Package**  
 Specify the Configuration Manager package that contains the PowerShell script. One package can contain multiple PowerShell scripts.  

 **Script name**  
 Specifies the name of the PowerShell script to run. This field is required.  

 **Parameters**  
 Specifies the parameters to be passed to the Windows PowerShell script. Configure the parameters as if you were adding them to the Windows PowerShell script from a command line.  

> [!IMPORTANT]  
>  Provide parameters consumed by the script, not for the Windows PowerShell command line.  
>   
>  The following example contains valid parameters:  
>   
>  **-MyParameter1 MyValue1 -MyParameter2 MyValue2**  
>   
>  The following example contains invalid parameters. The bold items are Windows PowerShell command-line parameters (-nologo and -executionpolicy unrestricted) and not consumed by the script.  
>   
>  **-nologo-executionpolicy unrestricted-File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2**  

 **PowerShell execution policy**  
 Select the PowerShell execution policy enables you to determine which Windows PowerShell scripts (if any) will be allowed to run on the computer. Choose one of the following execution policies:  

-   **AllSigned**: Only scripts signed by a trusted publisher can be run.  

-   **Undefined**: No execution policy is defined. .  

-   **Bypass**: Loads all configuration files and runs all scripts. If you run an unsigned script that was downloaded from the Internet, you are not prompted for permission before it runs.  

> [!IMPORTANT]  
>  PowerShell 1.0 does not support Undefined and Bypass execution policies.  

##  <a name="BKMK_SetDynamicVariables"></a> Set Dynamic Variables  
 Use the **Set Dynamic Variables** task sequence step to perform the following:  

1.  Gather information from the computer and the environment that it is in, and then set specified task sequence variables with the information.  

2.  Evaluate defined rules and set task sequence variables based on the variables and values configured for rules that evaluate to true.  

 The task sequence automatically sets the following read-only task sequence variables:  

 -   &#95;SMSTSMake  

 -   &#95;SMSTSModel  

 -   &#95;SMSTSMacAddresses  

 -   &#95;SMSTSIPAddresses  

 -   &#95;SMSTSSerialNumber  

 -   &#95;SMSTSAssetTag  

 -   &#95;SMSTSUUID  

 This step can be run in either a standard operating system or Windows PE. For more information about task sequence variables, see [Task sequence action variables](task-sequence-action-variables.md).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

**Name**  
 A short user-defined name for this task sequence step.  

**Description**  
 More detailed information about the action taken in this step.  

**Dynamic rules and variables**  
 To set a dynamic variable to use in the task sequence, you can add a rule and then specify a value for each variable that you specify for the rule or add one or more variables to set without adding a rule. When you add a rule, you can choose from the following rule categories:  

 -   **Computer**: Use this rule category to evaluate values for Asset tag, UUID, serial number, or mac address. You can set multiple values, and if any value is true, then the rule will evaluate to true. For example, the following rule evaluates to true if the Serial Number is 5892087 regardless of whether the MAC address equals 26-78-13-5A-A4-22.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Location**: Use this rule category to evaluate values for the default gateway.  

-   **Make and Model**: Use this rule category to evaluate values for the make and model of a computer. Both the make and model must evaluate to true for the rule to evaluate to true.   

    Starting in Configuration Manager version 1610, you can specify an asterisk (*****) and question mark (**?**) as wild cards, where ***** matches multiple characters and **?** matches a single character. For example, the string "DELL*900?" will match DELL-ABC-9001 and DELL9009.

-   **Task Sequence Variable**: Use this rule category to add a task sequence variable, condition, and value to evaluate. The rule evaluates to true when the value set for the variable meets the specified condition.  

You can specify one or more variables that will be set for a rule that evaluates to true or set variables without using a rule. You can select from existing variables or create a custom variable.  

 -   **Existing task sequence variables**: Use this setting to select one or more variables from a list of existing task sequence variables. Array variables are not available to select.  

 -   **Custom task sequence variables**: Use this setting to define a custom task sequence variable. You can also specify an existing task sequence variable. This is useful to specify an existing variable array, such as OSDAdapter, since variable arrays are not in the list of existing task sequence variables.  

After you select the variables for a rule, you must provide a value for each variable. The variable is set to the specified value when the rule evaluates to true. For each variable, you can select **Secret value** to hide the value of the variable. By default, some existing variables hide values, such as the OSDCaptureAccountPassword task sequence variable.  

> [!IMPORTANT]  
>  When you import a task sequence with the Set Dynamic Variables step, and **Secret value** is selected for the value of the variable, the value is removed when you import the task sequence. As a result, you must re-enter the value for the dynamic variable after you import the task sequence.  

##  <a name="BKMK_SetTaskSequenceVariable"></a> Set Task Sequence Variable  
Use the **Set Task Sequence Variable** task sequence step to set the value of a variable that is used with the task sequence.  

This step can be run in either a standard operating system or Windows PE. Task sequence variables are read by task sequence actions and specify the behavior of those actions. For more information about specific task sequence variables, see [Task sequence action variables](task-sequence-action-variables.md).  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name for this task sequence step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Task sequence variable**  
 A user-defined name for the task sequence variable.  

 **Value**  
 The value that is associated with the task sequence variable. The value could be another task sequence variable in %<varname\>% syntax.  

## Hide task sequence progress
<!-- 1354291 -->
With the 1706 release, you can control when task sequence progress is displayed to end users by using a new variable. In your task sequence, use the **Set Task Sequence Variable** step to set the value for the **TSDisableProgressUI** variable to hide or display task sequence progress. You can use the Set Task Sequence Variable step multiple times in a task sequence to change the value for the variable. This lets you hide or display task sequence progress in different sections of the task sequence.

 - **To hide task sequence progress**  
In task sequence editor, use the [Set Task Sequence Variable](#BKMK_SetTaskSequenceVariable) step to set the value of the **TSDisableProgressUI** variable to **True** to hide task sequence progress.

 - **To display task sequence progress**  
In task sequence editor, use the [Set Task Sequence Variable](#BKMK_SetTaskSequenceVariable) step to set the value of the **TSDisableProgressUI** variable to **False** to display task sequence progress.

##  <a name="BKMK_SetupWindowsandConfigMgr"></a> Setup Windows and ConfigMgr  
 Use the **Setup Windows and ConfigMgr** task sequence step to perform the transition from Windows PE to the new operating system. This task sequence step is a required part of any operating system deployment. It installs the Configuration Manager client into the new operating system and prepares for the task sequence to continue execution in the new operating system.  

 This step runs only in Windows PE. It does not run in a standard operating system. For more information about task sequence variables for this task sequence action, see [Setup Windows and ConfigMgr task sequence action variables](task-sequence-action-variables.md#BKMK_SetupWindows).  

 The **Setup Windows and ConfigMgr** task sequence action replaces sysprep.inf or unattend.xml directory variables, such as %WINDIR% and %ProgramFiles%, with the Windows PE installation directory X:\Windows. Task sequence variables specified by using these environment variables will be ignored.  

 Use this task sequence step to perform the following actions:  

1.  Preliminaries: Windows PE  

    1.  Performs task sequence variable substitution in the unattend.xml file.  

    2.  Downloads the package that contains the Configuration Manager client and puts it in the deployed image.  

2.  Set up Windows  

    1.  Image-based installation.  

        1.  Disables the Configuration Manager client in the image (that is, disables Autostart for the Configuration Manager client service).  

        2.  Updates the registry in the deployed image to ensure that the deployed operating system starts with the same drive letter that it had on the reference computer.  

        3.  Restarts in the deployed operating system.  

        4.  Windows mini-setup runs by using the previously specified sysprep.inf or unattend.xml file that has all end-user interaction suppressed. Note: If **Apply Network Settings** specified to join a domain, then that information is in the sysprep.inf or unattend.xml file, and Windows mini-setup performs the domain join.  

    2.  Setup.exe-based installation.  Runs Setup.exe that follows the typical Windows setup process:  

        1.  Copies the operating system install package specified in an earlier **Apply Operating System** task sequence to the hard disk drive.  

        2.  Restarts in the newly deployed operating system.  

        3.  Windows mini-setup runs by using the previously specified sysprep.inf or unattend.xml file that has all user interface settings suppressed. Note: If **Apply Network Settings** specified to join a domain, then that information is in the sysprep.inf or unattend.xml file, and Windows mini-setup performs the domain join.  

3.  Set up the Configuration Manager client  

    1.  After Windows mini-setup finishes, the task sequence resumes by using setupcomplete.cmd.  

    2.  Enables or disables the local administrator account, based on the option selected in the **Apply Windows Settings** step.  

    3.  Installs the Configuration Manager client by using the previously downloaded package (1.b) and installation properties specified in the Task Sequence Editor. The client is installed in "provisioning mode" to prevent it from processing new policy requests until the task sequence is completed.  

    4.  Waits for the client to be fully operational.  

    5.  If the computer is operating in an environment with Network Access Protection enabled, the client checks for and installs any required updates so that all required updates are present before the task sequence continues running.  

4.  The task sequence continues running with its next step.  

> [!NOTE]  
>  The **Setup Windows and ConfigMgr** task sequence action is responsible for running Group Policy on the newly installed computer. The  Group Policy is applied after the task sequence is finished.  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Do not select to have the task sequence continue if an error occurs while running the step. If there is an error, the task sequence will fail whether or not you select this setting.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 Specifies a short user-defined name that describes the action taken in this step.  

 **Description**  
 Specifies additional information about the action taken in this step.  

 **Client package**  
 Specifies the Configuration Manager client installation package that will be used by this task sequence step. Click **Browse** and select the client installation package that you want to use to install the Configuration Manager client.  

 **Use pre-production client package when available**  
 Specifies that if there is a pre-production client package available, that the task sequence step will use this package instead of the production client package. Typically, the pre-production client is a newer version that is being tested in the production environment. Click **Browse** and select the pre-production client installation package that you want to use to install the Configuration Manager client.  

 **Installation Properties**  
 Site assignment and the default configuration are automatically specified by the task sequence action. You can use this field to specify any additional installation properties to use when you install the client. To enter multiple installation properties, separate them with a space.  

 You can specify command-line options to use during client installation. For example, you can enter **/skipprereq: silverlight.exe** to inform CCMSetup.exe not to install the Microsoft Silverlight prerequisite. For more information about available command-line options for CCMSetup.exe, see [About client installation properties](../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="BKMK_UpgradeOS"></a> Upgrade Operating System  
 Use the **Upgrade Operating System** task sequence step to upgrade an existing Windows 7, Windows 8, Windows 8.1, or Windows 10 operating system to a Windows 10.  

 This task sequence step runs only in a standard operating system. It does not run in Windows PE.  

### Details  
 On the **Properties** tab for this step, you can configure the settings described in this section.  

 In addition, use the **Options** tab to do the following actions:  

-   Disable the step.  

-   Specify if the task sequence continues if an error occurs while running the step.  

-   Specify conditions that must be met for the step to run.  

 **Name**  
 A short user-defined name that describes the action taken in this step.  

 **Description**  
 More detailed information about the action taken in this step.  

 **Upgrade package**  
 Select this option to specify the Windows 10 operating system upgrade package to use for the upgrade.  

 **Source path**  
 Specifies a local or network path to the Windows 10 media that is to be used (corresponds to the /installFrom command-line option). You can also specify a variable, such as %mycontentpath% or %DPC01%. When you use a variable for the source path, it must be specified earlier in the task sequence. For example, if you use the [Download Package Content](#BKMK_DownloadPackageContent) step in the task sequence, you can specify a variable for the location of the operating system upgrade package. Then, you can use that variable for the source path for this step.  

 **Edition**  
 Specify the edition within the operating system media to use for the upgrade.  

 **Product key**  
 Specify the product key to apply to the upgrade process  

 **Provide the following driver content to Windows Setup during upgrade**  
 Select this setting to add drivers to the destination computer during the upgrade process (corresponds to the /InstallDriver command-line option). The drivers must be compatible with Windows 10. Specify one of the following:  

-   **Driver package**: Click **Browse** and select an existing driver package from the list.  

-   **Staged content**:  Select this option to specify the location for the driver package. You can specify a local folder, network path, or a task sequence variable. When you use a variable for the source path, it must be specified earlier in the task sequence. For example,  by using the [Download Package Content](task-sequence-steps.md#BKMK_DownloadPackageContent) step.  

 **Time-out (minutes)**  
 Specifies the number of minutes Setup has to run before Configuration Manager will fail the task sequence step.  

 **Perform Windows Setup compatibility scan without starting upgrade**  
 Specifies to perform the Windows Setup compatibility scan without starting the upgrade process (corresponds to the /Compat ScanOnly command-line option). You must still deploy the entire installation source when you use this option. Setup returns an exit code as a result of the scan. The following table provides some of the more common exit codes.  

|Exit code|Details|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|No compatibility issues ("success").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Actionable compatibility  issues.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|Selected migration choice is not available. For example, an upgrade from Enterprise to Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Not eligible for Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Not enough free disk space.|  

 For more information about this  parameter, see [Windows Setup Command-Line Options](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx)  

 **Ignore any dismissible compatibility messages**  
 Specifies that Setup completes the  installation, ignoring any dismissible compatibility messages (corresponds to the /Compat IgnoreWarning command-line option).  

 **Dynamically update Windows Setup with Windows Update**  
 Specifies whether setup will perform Dynamic Update operations, such as search, download, and install updates (corresponds to the /DynamicUpdate command-line option). This setting is not compatible with Configuration Manager software updates, but it can be enabled when you handle updates by using WSUS (stand-alone) or Windows Update.  

 **Override policy and use default Microsoft Update**: Select this setting to temporarily override the local policy in realtime to run Dynamic Update operations and have the computer get updates from Windows Update.  
