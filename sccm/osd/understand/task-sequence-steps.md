---
title: Task sequence steps
titleSuffix: Configuration Manager
description: Learn about the steps that you can add to a Configuration Manager task sequence.
ms.custom: na
ms.date: 03/30/2018
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
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Task sequence steps in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The following task sequence steps can be added to a Configuration Manager task sequence. For information about editing a task sequence, see [Edit a task sequence](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

The following settings are common to all task sequence steps:

On the **Properties** tab:
 - **Name**: The task sequence editor requires that you specify a short name to describe this step. When you add a new step, the task sequence editor sets the name to the Type by default. The **Name** length cannot exceed 50 characters.
 - **Description**: Optionally, specify more detailed information about this step. The **Description** length cannot exceed 256 characters.
The rest of this article describes the other settings on the **Properties** tab for each task sequence step.

On the **Options** tab:  
-   **Disable this step**: The task sequence skips this step when it runs on a computer. The icon for this step is greyed out in the task sequence editor. 
-   **Continue on error**: The task sequence continues if an error occurs while running the step.  
-   **Add Condition**: The task sequence evaluates these conditional statements to determine if it runs the step.   
The sections below for specific task sequence steps describe other possible settings on the **Options** tab.



##  <a name="BKMK_ApplyDataImage"></a> Apply Data Image   
 Use this step to copy the data image to the specified destination partition.  

 This step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables, see [Task sequence action variables](task-sequence-action-variables.md).  

In the task sequence editor, click **Add**, select **Images**, and select **Apply Data Image** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Image Package**  
 Click **Browse** to specify the **Image Package** used by this task sequence. Select the package you want to install in the **Select a Package** dialog box. The associated property information for each existing image package is displayed at the bottom of the **Select a Package** dialog box. Use the drop-down list to select the **Image** you want to install from the selected **Image Package**.  

> [!NOTE]  
>  This task sequence action treats the image as a data file. This action does not do any setup to boot the image as an operating system.  

 **Destination**  
 Configure one of the following options:

-   **Next available partition**: Use the next sequential partition that an **Apply Operating System** or **Apply Data Image** action in this task sequence has not already targeted.  

-   **Specific disk and partition**: Select the **Disk** number (starting with 0) and the **Partition** number (starting with 1).  

-   **Specific logical drive letter**: Specify the **Drive Letter** assigned to the partition by Windows PE. This drive letter can be different from the drive letter that the newly deployed operating system assigns.  

-   **Logical drive letter stored in a variable**: Specify the task sequence variable containing the drive letter assigned to the partition by Windows PE. This variable is typically set in the Advanced section of the **Partition Properties** dialog box for the **Format and Partition Disk** task sequence action.  

**Delete all content on the partition before applying the image**  
 Specifies that the task sequence deletes all files on the target partition before installing the image. By not deleting the content of the partition, this step can be used to apply additional content to a previously targeted partition.  



##  <a name="BKMK_ApplyDriverPackage"></a> Apply Driver Package  
 Use this step to download all of the drivers in the driver package and install them on the Windows operating system.

 The **Apply Driver Package** task sequence step makes all device drivers in a driver package available for use by Windows. Add this step between the **Apply Operating System** and **Setup Windows and ConfigMgr** steps to make the drivers in the package available to Windows. Typically, the **Apply Driver Package** step is placed after the **Auto Apply Drivers** task sequence step. The **Apply Driver Package** task sequence step is also useful with stand-alone media deployment scenarios.  

 Ensure that similar device drivers are put into a driver package and distribute them to the appropriate distribution points. After they are distributed, Configuration Manager client computers can install them. For example, put all drivers from one manufacturer into a driver package. Then distribute the package to distribution points where the associated computers can access them.

 The **Apply Driver Package** step is useful for stand-alone media. This step is also useful if you want to install a specific set of drivers. These types of drivers include devices that will not be detected in a plug-and-play scan, such as network printers.  

 This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Apply Driver Package Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

In the task sequence editor, click **Add**, select **Drivers**, and select **Apply Driver Package** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Driver package**  
 Specify the driver package that contains the needed device drivers by clicking **Browse** and launching the **Select a Package** dialog box. Specify an existing package to be made available. The associated package properties are displayed at the bottom of the dialog box.  

 **Select the mass storage driver within the package that needs to be installed before setup on pre-Windows Vista operating systems**  
 Specify any mass storage drivers needed to install a classic operating system.  

 **Driver**  
 Select the mass storage driver file to install before setup of a classic operating system. The drop-down list populates from the specified package.  

 **Model**  
 Specify the boot-critical device that is needed for pre-Windows Vista operating system deployments.  

 **Do unattended installation of unsigned drivers on version of Windows where this is allowed**  
 This option allows Windows to install drivers without a digital signature.  



##  <a name="BKMK_ApplyNetworkSettings"></a> Apply Network Settings   
 Use this step to specify the network or workgroup configuration information for the destination computer. The task sequence stores these values in the appropriate answer file. Windows Setup uses this answer file during the **Setup Windows and ConfigMgr** action.  

 This task sequence step runs in either a standard operating system or Windows PE. For more information about the task sequence variables for this action, see [Apply Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

 In the task sequence editor, click **Add**, select **Settings**, and select **Apply Network Settings** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Join a workgroup**  
 Select this option to have the destination computer join the specified workgroup. Enter the name of the workgroup on the **Workgroup** line. This value can be overridden by the value that is captured by the **Capture Network Settings** task sequence step.  

 **Join a domain**  
 Select this option to have the destination computer join the specified domain. Specify or browse to the domain, such as *fabricam.com*. Specify or browse to a Lightweight Directory Access Protocol (LDAP) path for an organizational unit. For example: *LDAP//OU=computers, DC=Fabricam.com, C=com*  

 **Account**  
 Click **Set** to specify an account with the necessary permissions to join the computer to the domain. In the **Windows User Account** dialog box you can enter the user name using the following format: **Domain\User**.  

 **Adapter settings**  
 Specify network configurations for each network adapter in the computer. Click **New** to open the **Network Settings** dialog box, and then specify the network settings. If you also use the **Capture Network Settings** step, the task sequence applies the previously captured settings to the network adapter. The task sequence does not apply the settings you specify in this step. If the task sequence did not previously capture network settings, it applies the settings specified in the **Apply Network Settings** step. The task sequence applies these settings to network adapters in Windows device enumeration order.  



##  <a name="BKMK_ApplyOperatingSystemImage"></a> Apply Operating System Image  

> [!TIP]  
> Beginning with Windows 10, version 1709, media includes multiple editions. When you configure a task sequence to use an OS upgrade package or OS image, be sure to select a [supported edition](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

 Use this step to install an operating system on the destination computer. This step performs actions depending on whether it uses an OS image or an OS upgrade package.  

 The **Apply Operating System Image** step performs the following actions when using an OS image:  

1.  Delete all content on the targeted volume, except files in the folder the &#95;SMSTSUserStatePath variable specifies.

2.  Extract the contents of the specified .wim file to the specified destination partition.  

3.  Prepare the answer file:  

    1.  Create a new default Windows Setup answer file (sysprep.inf or unattend.xml) for the operating system that is being deployed.  

    2.  Merge any values from the user-supplied answer file.  

4.  Copy Windows boot loaders into the active partition.  

5.  Set the boot.ini or the Boot Configuration Database (BCD) to reference the newly installed operating system.  

 The **Apply Operating System Image** step performs the following actions when using an OS upgrade package:  

1.  Delete all content on the targeted volume, except files in the folder the &#95;SMSTSUserStatePath variable specifies.  

2.  Prepare the answer file:  

    1.  Create a fresh answer file with standard values created by Configuration Manager.  

    2.  Merge any values from the user-supplied answer file.  

> [!NOTE]  
>  The **Setup Windows and ConfigMgr** step starts the installation of Windows. 

 After the **Apply Operating System** action runs, the OSDTargetSystemDrive variable is set to the drive letter of the partition containing the operating system files.  

 This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Apply Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

 In the task sequence editor, click **Add**, select **Images**, and select **Apply Operating System Image** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Apply operating system from a captured image**  
 Installs an operating system image that has previously been captured. Click **Browse** to open the **Select a package** dialog box, and then select the existing image package you want to install. If multiple images are associated with the specified **Image package**, use the drop-down list to specify the associated image to use for this deployment. You can view basic information about each existing image by clicking on the image.  

 **Apply operating system image from an original installation source**  
 Installs an operating system using an original installation source. Click **Browse** to open the **Select and Operating System Install Package** dialog box. Then select the existing OS upgrade package you want to use. You can view basic information about each existing image source by clicking on the image source. The associated image source properties are displayed in the results pane at the bottom of the dialog box. If there are multiple editions associated with the specified package, use the drop-down list to specify the associated **Edition** that is used.  

 **Use an unattended or sysprep answer file for a custom installation**  
 Use this option to provide a Windows setup answer file (**unattend.xml**, **unattend.txt**, or **sysprep.inf**) depending on the operating system version and installation method. The file you specify can include any of the standard configuration options supported by Windows answer files. For example, you can use it to specify the default Internet Explorer home page. Specify the package that contains the answer file and the associated path to the file in the package.  

> [!NOTE]  
>  The Windows setup answer file that you supply can contain embedded task sequence variables of the form %*varname*%, where *varname* is the name of the variable. The **Setup Windows and ConfigMgr** step substitutes the %*varname*% string for the actual variable values. These embedded task sequence variables cannot be used in numeric-only fields in an unattend.xml answer file.  

 If you do not supply a Windows setup answer file, this task sequence action automatically generates an answer file.  

 **Destination**  
 Configure one of the following options:  

-   **Next available partition**: Use the next sequential partition that an **Apply Operating System** or **Apply Data Image** action in this task sequence has not already targeted. 

-   **Specific disk and partition**: Select the **Disk** number (starting with 0) and the **Partition** number (starting with 1).  

-   **Specific logical drive letter**: Specify the **Drive Letter** assigned to the partition by Windows PE. This drive letter can be different from the drive letter that the newly deployed operating system assigns.  

-   **Logical drive letter stored in a variable**: Specify the task sequence variable containing the drive letter assigned to the partition by Windows PE. This variable is typically set in the Advanced section of the **Partition Properties** dialog box for the **Format and Partition Disk** task sequence action.  

### Options  
 Besides the default options, configure the following additional settings on the **Options** tab of this task sequence step:  

-   **Access content directly from the distribution point**  
     Configure the task sequence to access the operating system image directly from the distribution point. For example, use this option when you deploy operating systems to embedded devices that have limited storage capacity. When selecting this option, also configure the package share settings on the **Data Access** tab of the package properties.  

    > [!NOTE]  
    >  This setting overrides the deployment option that you configure on the **Distribution Points** page in the **Deploy Software Wizard**. This override is only for the OS image that this step specifies, not for all task sequence content.  



##  <a name="BKMK_ApplyWindowsSettings"></a> Apply Windows Settings  
 Use this step to configure the Windows settings for the destination computer. The task sequence stores these values in the appropriate answer file. Windows Setup uses this answer file during the **Setup Windows and ConfigMgr** action.  

 This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Apply Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

 In the task sequence editor, click **Add**, select **Settings**, and select **Apply Windows Settings** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **User name**  
 Specify the registered user name that is associated with the destination computer. This value can be overridden by the value that is captured by the **Capture Windows Settings** task sequence action.  

 **Organization name**  
 Specify the registered organization name that is associated with the destination computer. This value can be overridden by the value that is captured by the **Capture Windows Settings** task sequence action.  

 **Product key**  
 Specify the product key that is used for the Windows installation on the destination computer.  

 **Server licensing**  
 Specify the server licensing mode. You can select **Per server** or **Per user** as the licensing mode. If you select **Per server**, also specify the maximum number of connections permitted per your license agreement. Select **Do not specify** if the destination computer is not a server or you do not want to specify the licensing mode.  

 **Maximum connections**  
 Specify the maximum number of connections that are available for this computer as stated in your license agreement.  

 **Randomly generate the local administrator password and disable the account on all supported platforms (recommended)**  
 Select this option to set the local administrator password to a randomly-generated string. This option also disables the local administrator account on platforms that support this capability.  

 **Enable the account and specify the local administrator password**  
 Select this option to enable the local administrator account using the specified password. Enter the password on the **Password** line and confirm the password on the **Confirm password** line.  

 **Time Zone**  
 Specify the time zone to configure on the destination computer. This value can be overridden by the value that is captured by the **Capture Windows Settings** task sequence step.  



##  <a name="BKMK_AutoApplyDrivers"></a> Auto Apply Drivers  
 Use this step to match and install drivers as part of the operating system deployment.  

 The **Auto Apply Drivers** task sequence step performs the following actions:  

1.  Scan the hardware and find the plug-and-play IDs for all devices present on the system.  

2.  Send the list of devices and their plug-and-play IDs to the management point. The management point returns a list of compatible drivers from the driver catalog for each hardware device. The list includes all drivers regardless of what driver package they are in, drivers tagged with the specified driver category, and drivers not disabled.  

3.  For each hardware device, the task sequence picks the best driver. This driver is appropriate for the deployed operating system, and is on an accessible distribution point.  

4.  The task sequence downloads the selected drivers from a distribution point, and stages the drivers on the target operating system.  

    1.  For image-based installations, the task sequence places the drivers into the operating system driver store.  

    2.  For setup-based installations, the task sequence configures Windows Setup with the drivers' location.  

5.  During the **Setup Windows and ConfigMgr** step in the task sequence, Windows Setup finds the drivers staged by this action.  

> [!IMPORTANT]
>  Stand-alone media cannot use the **Auto Apply Drivers** step. Windows Setup has no connection to the Configuration Manager site in this scenario.

This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Auto Apply Drivers Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

 In the task sequence editor, click **Add**, select **Drivers**, and select **Auto Apply Drivers** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Install only the best matched compatible drivers**  
 Specifies that the task sequence step installs only the best matched driver for each hardware device detected.  

 **Install all compatible drivers**  
 The task sequence installs all drivers compatible for each detected hardware device. Windows Setup then chooses the best driver. This option takes more network bandwidth and disk space. The task sequence downloads more drivers, but Windows can select a better driver.  

 **Consider drivers from all categories**  
 The task sequence searches all available driver categories for the appropriate device drivers.  

 **Limit driver matching to only consider drivers in selected categories**  
 The task sequence searches in the specified driver categories for the appropriate device drivers.  

 **Do unattended installation of unsigned drivers on versions of Windows where this is allowed**  
 This option allows Windows to install drivers without a digital signature.   

  > [!IMPORTANT]  
  >  This option does not apply to operating systems where you cannot configure driver signing policy.  



##  <a name="BKMK_CaptureNetworkSettings"></a> Capture Network Settings  
 Use this step to capture Microsoft network settings from the computer running the task sequence. The task sequence saves these settings in task sequence variables. These settings override the default settings you configure on the **Apply Network Settings** step.  

 This task sequence step runs only in a standard operating system. It does not run in Windows PE. For more information about the task sequence variables for this action, see [Capture Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

In the task sequence editor, click **Add**, select **Settings**, and select **Capture Network Settings** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Migrate domain and workgroup membership**  
 Captures the domain and workgroup membership information of the destination computer.  

 **Migrate network adapter configuration**  
 Captures the network adapter configuration of the destination computer. The captured information includes the global network settings, the number of adapters, and the network settings associated with each adapter. These settings include settings associated with DNS, WINS, IP, and port filters.  



##  <a name="BKMK_CaptureOperatingSystemImage"></a> Capture Operating System Image  
 This step captures one or more images from a reference computer. The task sequence creates a Windows Image (.wim) file on the specified network share. Then use the **Add Operating System Image Package** wizard to import this image into Configuration Manager for image-based operating system deployments.  

 Configuration Manager captures each volume (drive) from the reference computer to a separate image within the .wim file. If the referenced computer has multiple volumes, the resulting .wim file contains a separate image for each volume. Only volumes that are formatted as NTFS or FAT32 are captured. Volumes with other formats and USB volumes are skipped.  

 The installed operating system on the reference computer must be a version of Windows that Configuration Manager supports. Use the SysPrep tool to prepare the reference computer operating system. The installed operating system volume and the boot volume must be the same volume.  

 Specify an account with write permissions to the selected network share.  

 This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Capture Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

 In the task sequence editor, click **Add**, select **Images**, and select **Capture Operating System Image** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

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
 Use this step to use the User State Migration Tool (USMT) to capture user state and settings from the computer running the task sequence. This task sequence step is used in conjunction with the **Restore User State** task sequence step. With USMT 3.0.1 and later, this option always encrypts the USMT state store by using an encryption key generated and managed by Configuration Manager.  

 For more information about managing the user state when deploying operating systems, see [Manage user state](../get-started/manage-user-state.md).  

 If you want to save and restore user state settings from a state migration point, use the **Capture User State** step with the **Request State Store** and **Release State Store** steps.  

 The **Capture User State** task sequence step provides control over a limited subset of the most commonly used USMT options. Additional command-line options can be specified using the OSDMigrateAdditionalCaptureOptions task sequence variable.  

 This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Capture User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureUserState).  

 In the task sequence editor, click **Add**, select **User State**, and select **Capture User State** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **User state migration tool package**  
 Specify the package that contains the User State Migration Tool (USMT). The task sequence uses this version of USMT to capture the user state and settings. This package does not require a program. Specify a package containing the 32-bit or 64-bit version of USMT. The architecture of USMT depends upon the architecture of the operating system from which the task sequence is capturing state.  

 **Capture all user profiles with standard options**  
 Migrate all user profile information. This is the default option.  

 If you select this option, but do not select **Restore local computer user profiles** in the **Restore User State** step, the task sequence fails. Configuration Manager cannot migrate the new accounts without assigning them passwords. 

 When you use the **Install an existing image package** option of the **New Task Sequence** wizard, the resulting task sequence defaults to **Capture all user profiles with standard options**. This default task sequence does not select the option to **Restore local computer user profiles**, in other words, non-domain user accounts.  

 Select **Restore local computer user profiles** and provide a password for the account to be migrated. In a manually created task sequence, this setting is found under the Restore User State step. In a task sequence created by the **New Task Sequence** wizard, this setting is found under the step **Restore User Files and Settings** wizard page.  

 If you have no local user accounts, this setting does not apply.  

 **Customize how user profiles are captured**  
 Select this option to specify a custom profile file migration. Click **Files** to select the configuration files for USMT to use with this step. Specify a custom .xml file that contains rules that define the user state files to migrate.  

 **Click here to select configuration files:**  
 Select this option to select the configuration files in the USMT package you want to use for capturing user profiles. Click the **Files** button to launch the **Configuration Files** dialog box. To specify a configuration file, enter the name of the file on the **Filename** line and click the **Add** button.  

 **Enable verbose logging**  
 Enable this option to generate more detailed log file information. When capturing state, the task sequence by default generates ScanState.log in the task sequence log folder, \windows\system32\ccm\logs.   

 **Skip files using encrypted file system**  
 Enable this option to skip capturing files encrypted with the Encrypted File System (EFS). These files include user profile files. Depending on the operating system and the USMT version, encrypted files might not be readable after you restore. For more information, see the USMT documentation.  

 **Copy by using file system access**  
 Enable this option to specify any of the following settings:  

-   **Continue if some files cannot be captured**: Enable this setting to continue the migration process even if some files cannot be captured. If you disable this option, if a file cannot be captured then this step fails. This option is enabled by default.  

-   **Capture locally by using links instead of by copying files**: Enable this setting to use NTFS hard-links to capture files.  

     For more information about migrating data using hard-links, see [Hard-Link Migration Store](http://go.microsoft.com/fwlink/p/?LinkId=240222)  

-   **Capture in off-line mode (Windows PE only)**: Enable this setting to capture the user state while in Windows PE instead of the full operating system.  
    
**Capture by using Volume Copy Shadow Services (VSS)**  
 This option allows you to capture files even if they are locked for editing by another application.  



##  <a name="BKMK_CaptureWindowsSettings"></a> Capture Windows Settings  
 Use this step to capture the Windows settings from the computer running the task sequence. The task sequence saves these settings in task sequence variables. These captured settings override the default settings that you configure on the **Apply Windows Settings** step.  

 This task sequence step runs in either Windows PE or a standard operating system. For more information about the task sequence variables for this action, see [Capture Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

 In the task sequence editor, click **Add**, select **Settings**, and select **Capture Windows Settings** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Migrate computer name**  
 Capture the NetBIOS computer name of the computer.  

 **Migrate registered user and organization names**  
 Capture the registered user and organization names from the computer.  

 **Migrate time zone**  
 Capture the time zone setting on the computer.  



##  <a name="BKMK_CheckReadiness"></a> Check Readiness  
 Use this step to verify that the target computer meets the specified deployment prerequisite conditions.  

In the task sequence editor, click **Add**, select **General**, and select **Check Readiness** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Ensure minimum memory (MB)**  
 Verify that the amount of memory, in megabytes (MB), meets or exceeds the specified amount. The step enables this setting by default.  

 **Ensure minimum processor speed (MHz)**  
 Verify that the speed of the processor, in megahertz (MHz), meets or exceeds the specified amount. The step enables this setting by default.  

 **Ensure minimum free disk space (MB)**  
 Verify that the amount of free disk space, in megabytes (MB), meets or exceeds the specified amount.  

 **Ensure current OS to be refreshed is**  
 Verify that the operating system installed on the target computer meets the specified requirement. The step sets this to **CLIENT** by default.  

### Options
 > [!NOTE]  
 > If you enable the **Continue on error** setting on the **Options** tab of this step, it only logs the readiness check results. If a check fails, the task sequence does not stop.



##  <a name="BKMK_ConnectToNetworkFolder"></a> Connect To Network Folder  
 Use this step to create a connection to a shared network folder.  

 This task sequence step runs in a standard operating system or Windows PE. For more information about the task sequence variables for this action, see [Connect to Network Folder Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

 In the task sequence editor, click **Add**, select **General**, and select **Connect To Network Folder** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Path**  
 Click **Browse** to specify the network folder path. Use the format *\\\server\share*.

 **Drive**  
 Select the local drive letter to assign for this connection. 

 **Account**  
 Click **Set** to specify the user account with permissions to connect to this network folder.



##  <a name="BKMK_DisableBitLocker"></a> Disable BitLocker  
 Use this step to disable the BitLocker encryption on the current operating system drive, or on a specific drive. This action leaves the key protectors visible in clear text on the hard drive, but it does not decrypt the contents of the drive. Consequently this action is completed almost instantly.  

> [!NOTE]  
>  BitLocker drive encryption provides low-level encryption of the contents of a disk volume.  

 If you have multiple drives encrypted, you must disable BitLocker on any data drives before disabling BitLocker on the operating system drive.  

 This step runs only in a standard operating system. It does not run in Windows PE.  

 In the task sequence editor, click **Add**, select **Disks**, and select **Disable BitLocker** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Current operating system drive**  
 Disables BitLocker on the current operating system drive.  

 **Specific drive**  
 Disables BitLocker on a specific drive. Use the drop-down list to specify the drive where BitLocker is disabled.  



##  <a name="BKMK_DownloadPackageContent"></a> Download Package Content  
 Use this step to download any of the following package types:  

-   Operating system images  

-   Operating system upgrade packages  

-   Driver packages  

-   Packages  

-   Boot images
    
This step works well in a task sequence to upgrade an operating system in the following scenarios:  

-   To use a single upgrade task sequence that can work with both x86 and x64 platforms. Include two **Download Package Content** steps in the **Prepare for Upgrade** group. Specify conditions on the **Options** tab to detect the client architecture and download only the appropriate OS upgrade package. Configure each **Download Package Content** step to use the same variable. Use the variable for the media path on the **Upgrade Operating System** step.  

-   To dynamically download an applicable driver package, use two **Download Package Content** steps with conditions to detect the appropriate hardware type for each driver package. Configure each **Download Package Content** step to use the same variable. Use the variable for the **Staged content** value in the Drivers section of the **Upgrade Operating System** step.  

> [!NOTE]    
> When you deploy a task sequence that contains the Download Package Content step, do not select **Download all content locally before starting the task sequence** or **Access content directly from a distribution point** for **Deployment options** on the **Distribution Points** page of the Deploy Software Wizard.  

This step runs in either a standard operating system or Windows PE. However, the option to save the package in the Configuration Manager client cache is not supported in WinPE.

 In the task sequence editor, click **Add**, select **Software**, and select **Download Package Content** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Select package** icon  
 Click the icon to select the package to download. After you select a package, you can click the icon again to choose another package.  

 **Place into the following location**  
 Choose to save the package in  one of the following locations:  

 -   **Task sequence working directory**  

 -   **Configuration Manager client cache**: Use this option to store the content in the client cache. The client acts as a peer cache source for other peer cache clients. For more information, see [Prepare Windows PE peer cache to reduce WAN traffic](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

 -    **Custom path**: With this option the task sequence engine first downloads the package to the task sequence working directory, then moves it to this path you specify. The task sequence engine appends the path with the package ID. 
   
**Save path as a variable**  
 You can save the path as a variable that you can  use in another task sequence step. Configuration Manager adds a numerical suffix to the variable name. For example, if you specify a variable of %*mycontent*% as a custom variable, it is the root for where the task sequence stores all referenced content. This content may contain multiple packages. Then when you refer to the variable, add a numerical suffix. For example, for the first package, refer to %*mycontent01*%. When you refer to the variable in subsequent steps, such as **Upgrade Operating System**, use %*mycontent02*% or %*mycontent03*%, where the number corresponds to the order that the **Download Package Content** step lists the packages.  

**If a package download fails, continue downloading other packages in the list**  
 If the task sequence fails to download a package, it starts to download the next package in the list.  



##  <a name="BKMK_EnableBitLocker"></a> Enable BitLocker  
Use this step to enable BitLocker encryption on at least two partitions on the hard drive. The first active partition contains the Windows bootstrap code. Another partition contains the operating system. The bootstrap partition must remain unencrypted.  

Use the **Pre-provision BitLocker** task sequence step to enable BitLocker on a drive while in Windows PE. For more information, see the [Pre-provision BitLocker](#BKMK_PreProvisionBitLocker) section.  

> [!NOTE]  
>  BitLocker drive encryption provides low-level encryption of the contents of a disk volume.  

The **Enable BitLocker** step runs only in a standard operating system. It does not run in Windows PE. For more information about the task sequence variables for this action, see [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

When you specify **TPM Only**, **TPM and Startup Key on USB**, or **TPM and PIN**, the Trusted Platform Module (TPM) must be in the following state before you can run the **Enable BitLocker** step:  

-   Enabled  
-   Activated  
-   Ownership Allowed  
   
This step completes any remaining TPM initialization. The remaining steps do not require physical presence or reboots. The **Enable BitLocker** step transparently completes the remaining TPM initialization steps, if necessary:  

-   Create endorsement key pair  
-   Create owner authorization value and escrow to Active Directory, which must have been extended to support this value  
-   Take ownership  
-   Create the storage root key, or reset if already present but incompatible  
   
If you want the task sequence to wait for the **Enable BitLocker** step to complete the drive encryption process, then select the **Wait** option. If you do not select the **Wait** option, the drive encryption process happens in the background. The task sequence immediately proceeds to the next step.  

BitLocker can be used to encrypt multiple drives on a computer system (both operating system and data drives). To encrypt a data drive, first encrypt the operating system drive and complete the encryption process. This requirement is because the operating system drive stores the key protectors for the data drives. If you encrypt the operating system and data drives in the same task sequence, select the **Wait** option on the **Enable BitLocker** step for the operating system drive.  

If the hard drive is already encrypted, but BitLocker is disabled, then the **Enable BitLocker** step re-enables the key protectors and completes quickly. Re-encryption of the hard drive is not necessary in this case.  

For more information about the task sequence variables for this action, see [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

In the task sequence editor, click **Add**, select **Disks**, and select **Enable BitLocker** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Choose the drive to encrypt**  
 Specifies the drive to encrypt. To encrypt the current operating system drive, select **Current operating system drive** and then configure one of the following options for key management:  

-   **TPM only**: Select this option to use only Trusted Platform Module (TPM).  

-   **Startup Key on USB only**: Select this option to use a startup key stored on a USB flash drive. When you select this option, BitLocker locks the normal boot process until a USB device that contains a BitLocker startup key is attached to the computer.  

-   **TPM and Startup Key on USB**: Select this option to use TPM and a startup key stored on a USB flash drive. When you select this option, BitLocker locks the normal boot process until a USB device that contains a BitLocker startup key is attached to the computer.  

-   **TPM and PIN**:  Select this option to use TPM and a personal identification number (PIN). When you select this option, BitLocker locks the normal boot process until the user provides the PIN.  
   
To encrypt a specific, non-operating system data drive, select **Specific drive**, and then select the drive from the list.  

**Chose where to create the recovery key**  
 To specify where BitLocker creates the recovery password and escrow it in Active Directory, select **In Active Directory**. If you select this option, you must extend Active Directory for the site. BitLocker can then save the associated recovery information in Active Directory. Select **Do not create recovery key** to not create a password. Creating a password is a best practice.  

**Wait for BitLocker to complete the drive encryption process on all drives before continuing task sequence execution**  
 Select this option to allow BitLocker drive encryption to complete prior to running the next step in the task sequence. If you select this option, BitLocker encrypts the entire disk volume before the user is able to log in to the computer.  

The encryption process can take hours to complete when encrypting a large hard drive. Not selecting this option allows the task sequence to proceed immediately.  



##  <a name="BKMK_FormatandPartitionDisk"></a> Format and Partition Disk  
 Use this step to format and partition a specified disk on the destination computer.  

> [!IMPORTANT]  
>  Every setting you specify for this task sequence step applies to a single specified disk. To format and partition another disk on the destination computer, add an additional **Format and Partition Disk** step to the task sequence.  

 This task sequence step runs only in Windows PE. It does not run in a standard operating system. For more information about the task sequence variables for this action, see [Format and Partition Disk Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

 In the task sequence editor, click **Add**, select **Disks**, and select **Format and Partition Disk** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Disk Number**  
 The physical disk number of the disk to format. The number is based on Windows disk enumeration ordering.  

 **Disk Type**  
 The type of the disk that is formatted. There are two options to select from the drop-down list: 

-   Standard(MBR) - Master Boot Record
-   GPT - GUID Partition Table  

> [!NOTE]  
>  If you change the disk type from **Standard (MBR)** to **GPT**, and the partition layout contains an extended partition, the task sequence removes all extended and logical partitions from the layout. The task sequence editor prompts to confirm this action before changing the disk type.  
   
**Volume**  
 Specific information about the partition or volume that the task sequence creates, including the following attributes:  

-   Name  
-   Remaining disk space  
   
To create a new partition, click **New** to launch the **Partition Properties** dialog box. Specify the partition type and size, and if it is a boot partition. To modify an existing partition, click the partition to be modified and then click the properties button. For more information about how to configure hard drive partitions, see one of the following articles:  

-   [How to Configure UEFI/GPT-Based Hard Drive Partitions](http://go.microsoft.com/fwlink/?LinkID=272104)  
-   [How to Configure BIOS/MBR-Based Hard Drive Partitions](http://go.microsoft.com/fwlink/?LinkId=272105)  

To delete a partition, select the partition to be deleted and then click **Delete**.  



##  <a name="BKMK_InstallApplication"></a> Install Application  
This step installs the specified applications, or a set of applications defined by a dynamic list of task sequence variables. When this step is run, the application installation begins immediately without waiting for a policy polling interval.  

The applications that are installed must meet the following criteria:  

-   The application must be a deployment type of Windows Installer or Script installer. Windows app package (.appx file) deployment types are not supported.  

-   It must run under the local system account and not the user account.  

-   It must not interact with the desktop. The program must run silently or in an unattended mode.  

-   It must not initiate a restart on its own. The application must request a restart by using the standard restart code, a 3010 exit code. This behavior ensures that the task sequence step correctly handles the restart. If the application does return a 3010 exit code, the underlying task sequence engine performs the restart. After the restart, the task sequence automatically continues.  

When the **Install Application** step runs, the application checks the applicability of the requirement rules and detection method on its deployment types. Based on the results of this check, the application installs the applicable deployment type. If a deployment type contains dependencies, the dependent deployment type is evaluated and installed as part of the install application step. Application dependencies are not supported for stand-alone media.  

> [!NOTE]  
>  To install an application that supersedes another application, the content files for the superseded application must be available. Otherwise this task sequence step fails. For example, Microsoft Visio 2010 is installed on a client or in a captured image. When the **Install Application** step installs Microsoft Visio 2013, the content files for Microsoft Visio 2010 (the superseded application) must be available on a distribution point. If Microsoft Visio is not installed at all on a client or captured image, the task sequence installs Microsoft Visio 2013 without checking for the Microsoft Visio 2010 content files.  

> [!NOTE]
> If the client fails to retrieve the management point list from location services, use the SMSTSMPListRequestTimeoutEnabled and SMSTSMPListRequestTimeout built-in variables to specify how many milliseconds a task sequence waits before it retries installing an application or software update. For more information, see [Task sequence built-in variables](task-sequence-built-in-variables.md).

 This task sequence step runs only in a standard operating system. It does not run in Windows PE.  

 In the task sequence editor, click **Add**, select **Software**, and select **Install Application** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings that are described in this section.  

 **Install the following applications**  
 The task sequence installs these applications in the specified order.  

 Configuration Manager filters out any disabled applications, or any applications with the following settings:  

-   Only when a user is logged on  
-   Run with user rights  

These applications do not appear in the **Select the application to install** dialog box.
  
**Install applications according to dynamic variable list**  
The task sequence installs applications using this base variable name. The base variable name is for a set of task sequence variables defined for a collection or computer. These variables specify the applications that the task sequence installs for that collection or computer. Each variable name consists of its common base name plus a numerical suffix starting at 01. The value for each variable must contain the name of the application and nothing else.  

For the task sequence to install applications by using a dynamic variable list, enable the following setting on the **General** tab of the application **Properties**: **Allow this application to be installed from the Install Application task sequence action instead of deploying manually**  

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

The following conditions affect the applications installed by the task sequence:  

-   If the value of a variable contains any information other than the name of the application. The task sequence does not install the application, and the task sequence continues.  

-   If the task sequence does not find a variable with the specified base name and "01" suffix, the task sequence does not install any applications. 
    
> [!Important]  
> These values are case-sensitive. For example, "install" is different than "Install". If you need to change the value, the task sequence editor doesn't detect a change of case. You must make another edit at the same time, for example, modify the step description.<!--509714-->   

   
**If an application fails, continue installing other applications in the list**  
 This setting specifies that the step continues when an individual application installation fails. If you specify this setting, the task sequence continues regardless of any installation errors. If you do not specify this setting, and the installation fails, the step immediately ends.  

### Options
 > [!NOTE] 
 > When you select **Continue on error** on the **Options** tab of this step, the task sequence continues when an application fails to install. When you do not enable this option, the task sequence fails and does not install remaining applications.  
 
Besides the default options, configure the following additional settings on the **Options** tab of this task sequence step:  

-   **Retry this step if computer unexpectedly restarts**  
    If one of the application installations unexpectedly restarts the computer, retry this step. The step enables this setting by default with two retries. You can specify from one to five retries.  



##  <a name="BKMK_InstallPackage"></a> Install Package
Use this step to install a software package as part of the task sequence. When this step is run, the installation begins immediately without waiting for a policy polling interval.  

The package must meet the following criteria:  

-   It must run under the local system account and not a user account.  

-   It should not interact with the desktop. The program must run silently or in an unattended mode.  

-   It must not initiate a restart on its own. The software must request a restart using the standard restart code, a 3010 exit code. This behavior ensures that the task sequence step properly handles the restart. If the software does return a 3010 exit code, the underlying task sequence engine restarts the computer. After the restart, the task sequence automatically continues.  

Programs that use the **Run another program first** option to install a dependent program are not supported when deploying an operating system. If you enable the package option **Run another program first**, and the dependent program already ran on the destination computer, the dependent program runs and the task sequence continues. However, if the dependent program has not already run on the destination computer, the task sequence step fails.  

> [!NOTE]  
>  The central administration site does not have the necessary client configuration policies required to enable the software distribution agent during the task sequence. When you create stand-alone media for a task sequence at the central administration site, and the task sequence includes an **Install Package** step, the following error might appear in the CreateTsMedia.log file:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  For stand-alone media that includes an **Install Package** step, create the stand-alone media at a primary site that has the software distribution agent enabled. Alternatively, add a **Run Command Line** step after the **Setup Windows and ConfigMgr** step and before the first **Install Package** step. The **Run Command Line** step runs a WMIC command to enable the software distribution agent before the first **Install Package** step. Use the following command in the **Run Command Line** step:  
>   
>  **Command Line**: `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>   
>  For more information about creating stand-alone media, see [Create stand-alone media](../deploy-use/create-stand-alone-media.md).  

This task sequence step runs only in a standard operating system. It does not run in Windows PE.  

In the task sequence editor, click **Add**, select **Software**, and select **Install Package** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Install a single software package**  
 This setting specifies a Configuration Manager software package. The step waits until the installation is complete.  

 **Install software packages according to dynamic variable list**  
 The task sequence installs packages using this base variable name. The base variable name is for a set of task sequence variables defined for a collection or computer. These variables specify the packages that the task sequence installs for that collection or computer. Each variable name consists of its common base name plus a numerical suffix starting at 001. The value for each variable must contain a package ID and the name of the software separated by a colon.  

 For the task sequence to install software by using a dynamic variable list, enable the following setting on the **Advanced** tab of the package **Properties**: **Allow this program to be installed from the Install Package task sequence without being deployed**  

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

 The following conditions affect the packages installed by the task sequence:  

-   If you do not create the value of a variable in the correct format, or it does not specify a valid package ID and name, the software installation fails.  

-   If the package ID contains lowercase characters, the software installation fails.  

-   If the task sequence does not find a variable with the specified base name and "001" suffix, the task sequence does not install any packages. The task sequence continues.  
    
> [!Important]  
> These values are case-sensitive. For example, "install" is different than "Install". If you need to change the value, the task sequence editor doesn't detect a change of case. You must make another edit at the same time, for example, modify the step description.<!--509714-->   

   
**If installation of a software package fails, continue installing other packages in the list**  
 This setting specifies that the step continues if an individual software package installation fails. If you specify this setting, the task sequence continues regardless of any installation errors. If you do not specify this setting, and the installation fails, the step immediately ends.  



##  <a name="BKMK_InstallSoftwareUpdates"></a> Install Software Updates  
Use this step to install software updates on the destination computer. The destination computer is not evaluated for applicable software updates until this task sequence step runs. At that time, the destination computer is evaluated for software updates like any other Configuration Manager client. For this step to install software updates, you must first deploy the updates to a collection of which the target computer is a member.  
>  [!IMPORTANT]
> A best practice for optimum performance is to install the latest version of the Windows Update Agent. 
>* For Windows 7, see [Knowledge base article 3161647](https://support.microsoft.com/kb/3161647).
>* For Windows 8, see [Knowledge base article 3163023](https://support.microsoft.com/kb/3163023).

 This task sequence step runs only in a standard operating system. It does not run in Windows PE. For information about task sequence variables for this task sequence action, see [Install Software Updates Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > If the client fails to retrieve the management point list from location services, use the SMSTSMPListRequestTimeoutEnabled and SMSTSMPListRequestTimeout built-in variables to specify how many milliseconds a task sequence waits before it retries installing an application or software update. For more information, see [Task sequence built-in variables](task-sequence-built-in-variables.md).

 In the task sequence editor, click **Add**, select **Software**, and select **Install Software Updates** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Required for installation - Mandatory software updates only**  
 Select this option to install all mandatory software updates with administrator-defined installation deadlines.  

 **Available for installation - All software updates**  
 Select this option to install all available software updates. You must first deploy these updates to a collection of which the computer is a member. The task sequence installs all available software updates on the destination computers.  

 **Evaluate software updates from cached scan results**  
 By default, the task sequence uses cached scan results from the Windows Update Agent. Clear the checkbox to instruct the Windows Update Agent to download the latest catalog from the software update point. Chose this option when using a task sequence to [capture and build an operating system image](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md). In this scenario a large number of software updates is likely. Many of these updates will have dependencies, for example, install X before Y appears as applicable. When you clear this setting and deploy the task sequence to many clients, they all connect to the software update point at the same time. This behavior results in performance issues during the process and download of the catalog. The best practice is the default setting to use cached scan results. 

The SMSTSSoftwareUpdateScanTimeout task sequence variable controls the software updates scan timeout during this step. The default value is 30 minutes. For more information, see [Task sequence built-in variables](task-sequence-built-in-variables.md).

### Options   
 Besides the default options, configure the following additional settings on the **Options** tab of this task sequence step:  

-   **Retry this step if computer unexpectedly restarts**  
    If one of the updates unexpectedly restarts the computer, retry this step. The step enables this setting by default with two retries. You can specify from one to five retries.  

    > [!NOTE]
    > Configure the SMSTSWaitForSecondReboot variable to specify how many seconds the task sequence pauses after the computer restarts in this scenario. For more information, see [Task sequence built-in variables](task-sequence-built-in-variables.md).



##  <a name="BKMK_JoinDomainorWorkgroup"></a> Join Domain or Workgroup  
 Use this step to add the destination computer to a workgroup or domain.  

 This task sequence step runs only in a standard operating system. It does not run in Windows PE. For information about task sequence variables for this task sequence action, see [Join Domain or Workgroup Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

 In the task sequence editor, click **Add**, select **General**, and select **Join Domain or Workgroup** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Join a workgroup**  
 Select this option to have the destination computer join the specified workgroup. If the computer is currently a member of a domain, selecting this option causes the computer to reboot.  

 **Join a domain**  
 Select this option to have the destination computer join the specified domain.  

 Optionally, enter or browse for an organizational unit (OU) in the specified domain for the computer to join. If the computer is currently a member of some other domain or a workgroup, this option causes the computer to reboot. If the computer is already a member of another OU, since Active Directory Domain Services does not allow changing the OU via this method, Windows Setup ignores this setting.  

 **Enter the account which has permission to join the domain**  
 Click **Set** to enter the username and password for an account with permissions to join the domain. Enter the account in the format:  *Domain\account*  



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Prepare ConfigMgr Client for Capture  
Use this step to remove or configure the Configuration Manager client on the reference computer. This action prepares the computer for capture as part of the imaging process.

Starting in Configuration Manager version 1610, the **Prepare ConfigMgr Client** step completely removes the Configuration Manager client, instead of only removing key information. When the task sequence deploys the captured operating system image, it installs a new Configuration Manager client each time.  

> [!Note]  
>  The task sequence engine only removes the client during the **Build and capture a reference operating system image** task sequence. The task sequence engine does not remove the client during other capture methods, such as capture media or a custom task sequence.

Prior to Configuration Manager version 1610, this step performs the following tasks:  

-   Removes the client configuration properties section from the smscfg.ini file in the Windows directory. These properties include client-specific information including the Configuration Manager GUID and other client identifiers.  

-   Deletes all SMS or Configuration Manager machine certificates.  

-   Deletes the Configuration Manager client cache.  

-   Clears the assigned site variable for the Configuration Manager client.  

-   Deletes all local Configuration Manager policy.  

-   Removes the trusted root key for the Configuration Manager client.  

This task sequence step runs only in a standard operating system. It does not run in Windows PE.  

In the task sequence editor, click **Add**, select **Images**, and select **Prepare ConfigMgr Client for Capture** to add this step. 

### Properties  
 This step does not require any settings on the **Properties** tab.



##  <a name="BKMK_PrepareWindowsforCapture"></a> Prepare Windows for Capture  
 Use this step to specify the Sysprep options when capturing an operating system image on the reference computer. This task sequence action runs Sysprep, and then reboots the computer into the Windows PE boot image specified for the task sequence. This action fails if the reference computer is joined to a domain.  

 This task sequence step runs only in a standard operating system. It does not run in Windows PE. For information about task sequence variables for this task sequence action, see [Prepare Windows for Capture Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

 In the task sequence editor, click **Add**, select **Images**, and select **Prepare Windows for Capture** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Automatically build mass storage driver list**  
 Select this option to have Sysprep automatically build a list of mass storage drivers from the reference computer. This option enables the Build Mass Storage Drivers option in the sysprep.inf file on the reference computer. For more information about this setting, see the Sysprep documentation.  

 **Do not reset activation flag**  
 Select this option to prevent Sysprep from resetting the product activation flag.  



##  <a name="BKMK_PreProvisionBitLocker"></a> Pre-provision BitLocker  
 Use this step to enable BitLocker on a drive while in Windows PE. Only the used drive space is encrypted, and therefore, encryption times are much faster. You apply the key management options by using the [Enable BitLocker](#BKMK_EnableBitLocker) task sequence step after the operating system installs. This step runs only in Windows PE. It does not run in a standard operating system.  

> [!IMPORTANT]  
>  Pre-provisioning BitLocker requires at least Windows 7. The computer must also contain a supported and enabled Trusted Platform Module (TPM).  

 In the task sequence editor, click **Add**, select **Disks**, and select **Pre-provision BitLocker** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Apply BitLocker to the specified drive**  
 Specify the drive for which you want to enable BitLocker. Only the used space on the drive is encrypted.  

 **Skip this step for computers that do not have a TPM or when TPM is not enabled**  
 Select this option to skip drive encryption on a computer that does not contain a supported or enabled TPM as required. For example, use this option when you deploy an operating system to a virtual machine.  



##  <a name="BKMK_ReleaseStateStore"></a> Release State Store  
 Use this step to notify the state migration point that the capture or restore action is complete. Use this step in conjunction with the **Request State Store**, **Capture User State**, and **Restore User State** steps. You use these steps to migrate user state data using a state migration point and the User State Migration Tool (USMT).  

 For more information about managing the user state when deploying operating systems, see [Manage user state](../get-started/manage-user-state.md).  

 If you use the **Request State Store** step to request access to a state migration point to *capture* user state, this step notifies the state migration point that the capture process is complete. The state migration point then marks the user state data as available for restore. The state migration point sets the access control permissions for the user state data so that only the restoring computer has read-only access.  

 If you use the **Request State Store** step to request access to a state migration point to *restore* user state, this step notifies the state migration point that the restore process is complete. The state migration point then activates its configured data retention settings.  

> [!IMPORTANT]  
>  A best practice is to set the **Continue on Error** option for any steps between the **Request State Store** and **Release State Store** steps. Every **Request State Store** step must have a matching **Release State Store** step.  

 This task sequence step runs only in a standard operating system. It does not run in Windows PE. For information about task sequence variables for this task sequence action, see [Release State Store Sequence Action Variables](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

 In the task sequence editor, click **Add**, select **User State**, and select **Release State Store** to add this step. 

### Properties  
 This step does not require any settings on the **Properties** tab.



##  <a name="BKMK_RequestStateStore"></a> Request State Store  
 Use this step to request access to a state migration point when capturing or restoring state.  

 For more information about managing the user state when deploying operating systems, see [Manage user state](../get-started/manage-user-state.md).  

 Use this step in conjunction with the **Release State Store**, **Capture User State**, and **Restore User State** steps. You use these steps to migrate computer state using a state migration point and the User State Migration Tool (USMT).  

> [!NOTE]  
>  When creating a new state migration point, user state storage is not available for up to one hour. To expedite availability, adjust any property settings on the state migration point to trigger a site control file update.  

 This task sequence step runs in a standard operating system and in Windows PE for offline USMT. For information about the task sequence variables for this task sequence action, see [Request State Store Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RequestState).  

In the task sequence editor, click **Add**, select **User State**, and select **Request State Store** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Capture state from the computer**  
 Find a state migration point that meets the minimum requirements as configured in the state migration point settings. For example, **Maximum number of clients** and **Minimum amount of free disk space**. This option does not guarantee sufficient space is available at the time of state migration. This option requests access to the state migration point for the purpose of capturing the user state and settings from a computer.  

 If the Configuration Manager site has multiple active state migration points, this step finds a state migration point with available disk space. The task sequence queries the management point for a list of state migration points, and then evaluates each until it finds one that meets the minimum requirements.  

 **Restore state from another computer**  
 Request access to a state migration point to restore previously captured user state and settings to a destination computer.  

 If there are multiple state migration points, this step finds the state migration point that has the state for the destination computer.  

 **Number of retries**  
 The number of times that this step tries to find an appropriate state migration point before failing.  

 **Retry delay (in seconds)**  
 The amount of time in seconds that the task sequence step waits between retry attempts.  

 **If computer account fails to connect to a state store, use the network access account.**  
 If the task sequence cannot access the state migration point using the computer account, it uses the network access account credentials to connect. This option is less secure because other computers could use the network access account to access the stored state. This option might be necessary if the destination computer is not domain joined.  



##  <a name="BKMK_RestartComputer"></a> Restart Computer  
 Use this step to restart the computer running the task sequence. After the restart, the computer automatically continues with the next step in the task sequence.  

 This step can be run in either a standard operating system or Windows PE. For more information about the task sequence variables for this task sequence action, see [Restart computer task sequence action variables](task-sequence-action-variables.md#BKMK_RestartComputer).  

 In the task sequence editor, click **Add**, select **General**, and select **Restart Computer** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **The boot image assigned to this task sequence**  
 Select this option for the destination computer to use the boot image assigned to the task sequence. The task sequence uses the boot image to run subsequent steps in Windows PE.  

 **The currently installed default operating system**  
 Select this option for the destination computer to reboot into the installed operating system.  

 **Notify the user before restarting**  
 Select this option to display a notification to the user before the destination computer restarts. The step selects this option by default.  

 **Notification message**  
 Enter a notification message to display to the user before the destination computer restarts.  

 **Message display time-out**  
 Specify the amount of time in seconds before the destination computer restarts. The default is 60 seconds.  



##  <a name="BKMK_RestoreUserState"></a> Restore User State  
 Use this step to initiate the User State Migration Tool (USMT) to restore user state and settings to the destination computer. You use this step in conjunction with the **Capture User State** step.  

 For more information about managing the user state when deploying operating systems, see [Manage user state](../get-started/manage-user-state.md).  

 Use this step with the **Request State Store** and **Release State Store** steps to save or restore the state settings with a state migration point. With USMT 3.0 and above, this option always decrypts the USMT state store by using an encryption key generated and managed by Configuration Manager.  

 The **Restore User State** step provides control over a limited subset of the most commonly used USMT options. Specify additional command-line options with the OSDMigrateAdditionalRestoreOptions task sequence variable.  

> [!IMPORTANT]  
>  If you are using this step for a purpose unrelated to an operating system deployment scenario, add the [Restart Computer](#BKMK_RestartComputer) step immediately following the **Restore User State** step.  

 This step runs only in a standard operating system. It does not run in Windows PE. For information about the task sequence variables for this task sequence action, see [Restore User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RestoreUserState).  

 In the task sequence editor, click **Add**, select **User State**, and select **Restore User State** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **User state migration tool package**  
 Specify the package that contains the version of USMT for this step to use. This package does not require a program. When the step runs, the task sequence uses the version of USMT in the specified package. Specify a package containing the 32-bit or 64-bit version of USMT. The architecture of USMT depends upon the architecture of the operating system to which the task sequence is restoring state. 

 **Restore all captured user profiles with standard options**  
 Restores the captured user profiles with the standard options. To customize the options that USMT restores, select **Customize user profile capture**.  

 **Customize how user profiles are restored**  
 Allows you to customize the files that you want to restore to the destination computer. Click **Files** to specify the configuration files in the USMT package you want to use for restoring the user profiles. To add a configuration file, enter the name of the file in the **Filename** box, and then click **Add**. The Files pane lists the configuration files that USMT uses. The .xml file you specify defines which user file USMT restores.  

 **Restore local computer user profiles**  
 Restores the local computer user profiles. These profiles are not for domain users. You must assign new passwords to the restored local user accounts. USMT cannot migrate the original passwords. Enter the new password in the **Password** box, and confirm the password in the **Confirm Password** box.  

 **Continue if some files cannot be restored**  
 Continues restoring user state and settings even if USMT is unable to restore some files. The step enables this option by default. If you disable this option and USMT encounters errors while restoring files, this step fails immediately. USMT does not restore all files.   

 **Enable verbose logging**  
 Enable this option to generate more detailed log file information. When restoring state, the task sequence by default generates Loadstate.log in the task sequence log folder, \windows\system32\ccm\logs.  



##  <a name="BKMK_RunCommandLine"></a> Run Command Line  
 Use this step to run the specified command line.  

 This step can be run in a standard operating system or Windows PE. For information about task sequence variables for this task sequence action, see [Run Command Line Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RunCommand).  

 In the task sequence editor, click **Add**, select **General**, and select **Run Command Line** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Command line**  
 Specifies the command line that is run. This field is required. Including file name extensions are a best practice, for example, .vbs and .exe. Include all required settings files, command-line options, or switches.  

 If the file name does not have a file name extension specified, Configuration Manager tries .com, .exe, and .bat. If the file name has an extension that is not an executable, Configuration Manager tries to apply a local association. For example, if the command line is readme.gif, Configuration Manager starts the application specified on the destination computer for opening .gif files.  

 Examples:  

 `setup.exe /a`  

 `cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
>  To run successfully, precede command-line actions with the **cmd.exe /c** command. Example of these actions include output redirection, piping, and copy commands.  

 **Disable 64-bit file system redirection**  
 64-bit operating systems use the WOW64 file system redirector by default to run command lines. This behavior is to properly find 32-bit versions of operating system executables and libraries. Select this option to disable the use of the WOW64 file system redirector. Windows runs the command using native 64-bit versions of operating system executables and libraries. This option has no effect when running on a 32-bit operating system.  

 **Start in**  
 Specifies the executable folder for the program, up to 127 characters. This folder can be an absolute path on the destination computer or a path relative to the distribution point folder that contains the package. This field is optional.  

 Examples:  

 **c:\officexp**  

 **i386**  

> [!NOTE]  
>  The **Browse** button browses the local computer for files and folders. Anything you select must also exist on the destination computer in the same location and with the same file and folder names.  

 **Package**  
 When you specify files or programs on the command line that are not already present on the destination computer, select this option to specify the Configuration Manager package that contains the appropriate files. The package does not require a program. This option is not required if the specified files exist on the destination computer.  

 **Time-out**  
 Specifies a value that represents how long Configuration Manager allows the command line to run. This value can be from 1 minute to 999 minutes. The default value is 15 minutes.  

 This option is disabled by default.  

> [!IMPORTANT]  
>  If you enter a value that does not allow enough time for the specified command to complete successfully, this step fails. The entire task sequence could fail depending on other control settings. If the time-out expires, Configuration Manager terminates the command-line process.  

 **Run this step as the following account**  
 Specifies that the command line is run as a Windows user account other than the local system account.  

> [!NOTE]  
>  To run simple scripts or commands with another account after installing the operating system, you must first add the account to the computer. Additionally, you must restore the Windows user account profile to run more complex programs, such as a Windows Installer.  

 **Account**  
 Specifies the Windows user account this step uses to run the command-line. The command line runs with the permissions of the specified account. Click **Set** to specify the local user or domain account.  

> [!IMPORTANT]  
>  If this step specifies a user account and runs in Windows PE, the action fails. You cannot join Windows PE to a domain. The smsts.log file records this failure.  



##  <a name="BKMK_RunPowerShellScript"></a> Run PowerShell Script  
 Use this step to run the specified PowerShell script.  

 This step can be run in a standard operating system or Windows PE. To run this step in Windows PE, PowerShell must be enabled in the boot image. You can enable Windows PowerShell (WinPE-PowerShell) from the **Optional Components** tab in the properties for the boot image. For more information about how to modify a boot image, see [Manage boot images](../get-started/manage-boot-images.md).  

> [!NOTE]  
>  PowerShell is not enabled by default on Windows Embedded operating systems.  

In the task sequence editor, click **Add**, select **General**, and select **Run PowerShell Script** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Package**  
 Specify the Configuration Manager package that contains the PowerShell script. One package can contain multiple PowerShell scripts.  

 **Script name**  
 Specifies the name of the PowerShell script to run. This field is required.  

 **Parameters**  
 Specifies the parameters passed to the Windows PowerShell script. These parameters are the same as the Windows PowerShell script parameters on the command line.  

> [!IMPORTANT]  
>  Provide parameters consumed by the script, not for the Windows PowerShell command line.  
>   
>  The following example contains valid parameters:  
>   
>  `-MyParameter1 MyValue1 -MyParameter2 MyValue2`  
>   
>  The following example contains invalid parameters. The first two items are Windows PowerShell command-line parameters (**-NoLogo** and **-ExecutionPolicy Unrestricted**). The script does not consume these parameters.  
>   
>  `-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`  

 **PowerShell execution policy**  
 Determine which Windows PowerShell scripts (if any) you allow to run on the computer. Choose one of the following execution policies:  

-   **AllSigned**: Only run scripts signed by a trusted publisher  

-   **Undefined**: Do not define any execution policy  

-   **Bypass**: Load all configuration files and run all scripts. If you download an unsigned script from the Internet, Windows PowerShell does not prompt for permission before running the script.  

> [!IMPORTANT]  
>  PowerShell 1.0 does not support Undefined and Bypass execution policies.  



##  <a name="child-task-sequence"></a> Run Task Sequence

Beginning with Configuration Manager version 1710, you can add a new step that runs another task sequence. This step creates a parent-child relationship between the task sequences. With child task sequences, you can create more modular, reusable task sequences.

Consider the following statements when you add a child task sequence to a task sequence:
 - The parent and child task sequences are effectively combined into a single policy that the client runs.
 - The environment is global. If the parent task sequence sets a variable, and then the child task sequence changes that variable, it retains the latest value. If the child task sequence creates a new variable, it is available for the rest of the parent task sequence.
 - Status messages are sent per normal for a single task sequence operation.
 - The task sequences write entries to the smsts.log file, with new log entries that make it clear when a child task sequence starts.

In the task sequence editor, click **Add**, select **General**, and select **Run Task Sequence** to add this step. 

### Properties
 On the **Properties** tab for this step, configure the settings described in this section.  

**Select task sequence to run**  
 Click **Browse** to select the child task sequence. The **Select a Task Sequence** dialog box does not display the parent task sequence.



##  <a name="BKMK_SetDynamicVariables"></a> Set Dynamic Variables  
 Use this step to perform the following actions:  

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

In the task sequence editor, click **Add**, select **General**, and select **Set Dynamic Variables** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

**Dynamic rules and variables**  
 To set a dynamic variable for use in the task sequence, add a rule. Then set a value for each variable specified in the rule. Additionally, add one or more variables without adding a rule. When you add a rule, choose from the following categories:  

 -   **Computer**: Evaluate values for hardware asset tag, UUID, serial number, or MAC address. Set multiple values as necessary. If any value is true, then the rule evaluates as true. For example, the following rule evaluates as true if the device serial number is 5892087 and the MAC address is 22-A4-5A-13-78-26.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Location**: Evaluate values for the default network gateway  

-   **Make and Model**: Evaluate values for the make and model of a computer. Both the make and model must evaluate to true for the rule to evaluate to true.   

    <!-- for future edits: an escape code must be used for the bolded asterisk character, but may be removed somewhere along the way. Instead of five asterisk, should be bold tags with &#42; in-between -->

    Starting in Configuration Manager version 1610, you can specify an asterisk (**&#42;**) and question mark (**?**) as wild cards, where **&#42;** matches multiple characters and **?** matches a single character. For example, the string "DELL*900?" will match DELL-ABC-9001 and DELL9009. 

    Specify an asterisk (**&#42;**) and question mark (**?**) as wild cards, where **&#42;** matches multiple characters and **?** matches a single character. For example, the string "DELL*900?" matches DELL-ABC-9001 and DELL9009.

-   **Task Sequence Variable**: Add a task sequence variable, condition, and value to evaluate. The rule evaluates to true when the value set for the variable meets the specified condition.  

    Specify one or more variables to set for a rule that evaluates to true, or set variables without using a rule. Select an existing variable, or create a custom variable.  

     -   **Existing task sequence variables**: Select one or more variables from a list of existing task sequence variables. Array variables are not available to select.  

     -   **Custom task sequence variables**: Define a custom task sequence variable. You can also specify an existing task sequence variable. This setting is useful to specify an existing variable array, such as OSDAdapter, since variable arrays are not in the list of existing task sequence variables.  

After you select the variables for a rule, you must provide a value for each variable. The variable is set to the specified value when the rule evaluates to true. For each variable, you can select **Secret value** to hide the value of the variable. By default, some existing variables hide values, such as the OSDCaptureAccountPassword task sequence variable.  

> [!IMPORTANT]  
>  Configuration Manager removes any variable values marked as a **Secret value** when you import a task sequence with the **Set Dynamic Variables** step. Re-enter the value for the dynamic variable after you import the task sequence.  



##  <a name="BKMK_SetTaskSequenceVariable"></a> Set Task Sequence Variable  
Use this step to set the value of a variable that is used with the task sequence.  

This step can be run in either a standard operating system or Windows PE. Task sequence variables are read by task sequence actions and specify the behavior of those actions. For more information about specific task sequence action variables, see [Task sequence action variables](task-sequence-action-variables.md). For more information about specific task sequence built-in variables, see [Task sequence built-in variables](/sccm/osd/understand/task-sequence-built-in-variables).

In the task sequence editor, click **Add**, select **General**, and select **Set Task Sequence Variable** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Task sequence variable**  
 Specify the name of a task sequence built-in or action variable, or specify your own user-defined variable name.  

 **Value**  
 The task sequence sets the variable to this value. Set this task sequence variable to the value of another task sequence variable with the syntax %varname%.  



##  <a name="BKMK_SetupWindowsandConfigMgr"></a> Setup Windows and ConfigMgr  
 Use this step to perform the transition from Windows PE to the new operating system. This task sequence step is a required part of any operating system deployment. It installs the Configuration Manager client into the new operating system and prepares for the task sequence to continue execution in the new operating system.  

 This step runs only in Windows PE. It does not run in a standard operating system. For more information about task sequence variables for this task sequence action, see [Setup Windows and ConfigMgr task sequence action variables](task-sequence-action-variables.md#BKMK_SetupWindows).  

 This step replaces sysprep.inf or unattend.xml directory variables, such as %WINDIR% and %ProgramFiles%, with the Windows PE installation directory, X:\Windows. The task sequence ignores variables specified by using these environment variables.  

 Use this task sequence step to perform the following actions:  

1.  Preliminaries: Windows PE  

    1.  Substitute task sequence variables in the unattend.xml file.  

    2.  Download the package that contains the Configuration Manager client. Add the package to the deployed image.  

2.  Set up Windows  

    1.  Image-based installation  

        1.  Disable the Configuration Manager client in the image, if it exists. In other words, disable Autostart for the Configuration Manager client service.  

        2.  Update the registry in the deployed image to start the deployed operating system with the same drive letter as the reference computer.  

        3.  Restart to the deployed operating system.  

        4.  Windows mini-setup runs by using the previously specified sysprep.inf or unattend.xml answer file that has all end-user interaction suppressed. If you use the **Apply Network Settings** step to join a domain, then that information is in the answer file. Windows mini-setup joins the computer to the domain.  

    2.  Setup.exe-based installation.  Runs Setup.exe that follows the typical Windows setup process:  

        1.  Copy the OS upgrade package, specified in the **Apply Operating System** step, to the hard disk drive.  

        2.  Restart to the newly deployed operating system.  

        3.  Windows mini-setup runs by using the previously specified sysprep.inf or unattend.xml answer file that has all user interface settings suppressed. If you use the  **Apply Network Settings** step to join a domain, then that information is in the answer file. Windows mini-setup joins the computer to the domain.  

3.  Set up the Configuration Manager client  

    1.  After Windows mini-setup finishes, the task sequence resumes by using setupcomplete.cmd.  

    2.  Enable or disable the local administrator account, based on the option selected in the **Apply Windows Settings** step.  

    3.  Install the Configuration Manager client by using the previously downloaded package, and installation properties specified in this step. The client installs in "provisioning mode" to prevent it from processing new policy requests until the task sequence completes.  

    4.  Wait for the client to be fully operational.  

4.  The task sequence continues running the next step.  

<!-- Engineering confirmed that the task sequence does nothing with respect to group policy processing.
> [!NOTE]  
>  The **Setup Windows and ConfigMgr** task sequence action is responsible for running Group Policy on the newly installed computer. The Group Policy is applied after the task sequence is finished.  
-->

In the task sequence editor, click **Add**, select **Images**, and select **Setup Windows and ConfigMgr** to add this step. 

### Properties  
 On the **Properties** tab for this step, configure the settings described in this section.  

 **Client package**  
 Click **Browse**, then select the Configuration Manager client installation package to use with this step.  

 **Use pre-production client package when available**  
 If there is a pre-production client package available, and the computer is a member of the piloting collection, the task sequence uses this package instead of the production client package. The pre-production client is a newer version for testing in the production environment. Click **Browse**, then select the pre-production client installation package to use with this step.  

 **Installation Properties**  
 Site assignment and the default configuration are automatically specified by the task sequence action. You can use this field to specify any additional installation properties to use when you install the client. To enter multiple installation properties, separate them with a space.  

 You can specify command-line options to use during client installation. For example, you can enter **/skipprereq: silverlight.exe** to inform CCMSetup.exe not to install the Microsoft Silverlight prerequisite. For more information about available command-line options for CCMSetup.exe, see [About client installation properties](../../core/clients/deploy/about-client-installation-properties.md).  

### Options
> [!NOTE]
> Do not enable **Continue on error** on the **Options** tab. If there is an error during this step, the task sequence fails whether or not you enable this setting.



##  <a name="BKMK_UpgradeOS"></a> Upgrade Operating System  
 > [!TIP]  
 > Beginning with Windows 10, version 1709, media includes multiple editions. When you configure a task sequence to use an OS upgrade package or OS image, be sure to select a [supported edition](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

 Use this step to upgrade an older version of Windows to a newer version of Windows 10.  

 This task sequence step runs only in a standard operating system. It does not run in Windows PE.  

In the task sequence editor, click **Add**, select **Images**, and select **Upgrade Operating System** to add this step. 

### Properties  
On the **Properties** tab for this step, configure the settings described in this section.  

**Upgrade package**  
 Select this option to specify the Windows 10 operating system upgrade package to use for the upgrade.  

**Source path**  
 Specifies a local or network path to the Windows 10 media that Windows Setup uses. This setting corresponds to the Windows Setup command-line option **/InstallFrom**. You can also specify a variable, such as %mycontentpath% or %DPC01%. When you use a variable for the source path, it must be specified earlier in the task sequence. For example, if you use the [Download Package Content](#BKMK_DownloadPackageContent) step in the task sequence, you can specify a variable for the location of the operating system upgrade package. Then, you can use that variable for the source path for this step.  

**Edition**  
 Specify the edition within the operating system media to use for the upgrade.  

**Product key**  
 Specify the product key to apply to the upgrade process  

**Provide the following driver content to Windows Setup during upgrade**  
 Add drivers to the destination computer during the upgrade process. This setting corresponds to the Windows Setup command-line option **/InstallDriver**. The drivers must be compatible with Windows 10. Specify one of the following options:  

-   **Driver package**: Click **Browse** and select an existing driver package from the list.  

-   **Staged content**:  Select this option to specify the location for the driver package. You can specify a local folder, network path, or a task sequence variable. When you use a variable for the source path, it must be specified earlier in the task sequence. For example,  by using the [Download Package Content](task-sequence-steps.md#BKMK_DownloadPackageContent) step.  

**Time-out (minutes)**  
 Specifies the number of minutes before Configuration Manager fails this step. This option is useful if Windows Setup stops processing but does not terminate.  

**Perform Windows Setup compatibility scan without starting upgrade**  
 Perform the Windows Setup compatibility scan without starting the upgrade process. This setting corresponds to the Windows Setup command-line option **/Compat ScanOnly**. You must deploy the entire installation source when you use this option. Setup returns an exit code as a result of the scan. The following table provides some of the more common exit codes.  

|Exit code|Details|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|No compatibility issues ("success").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Actionable compatibility  issues.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|Selected migration choice is not available. For example, an upgrade from Enterprise to Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Not eligible for Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Not enough free disk space.|  

For more information about this  parameter, see [Windows Setup Command-Line Options](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx)  

**Ignore any dismissible compatibility messages**  
 Specifies that Setup completes the installation, ignoring any dismissible compatibility messages. This setting corresponds to the Windows Setup command-line option **/Compat IgnoreWarning**.  

**Dynamically update Windows Setup with Windows Update**  
 Enable setup to perform Dynamic Update operations, such as search, download, and install updates. This setting corresponds to the Windows Setup command-line option **/DynamicUpdate**. This setting is not compatible with Configuration Manager software updates. Enable this option when you manage updates with stand-alone Windows Server Update Services (WSUS) or Windows Update for Business.  

**Override policy and use default Microsoft Update**
 Temporarily override the local policy in real-time to run Dynamic Update operations and have the computer get updates from Windows Update.
