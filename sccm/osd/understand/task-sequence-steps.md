---
title: Task sequence steps
titleSuffix: Configuration Manager
description: Learn about the steps that you can add to a Configuration Manager task sequence.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Task sequence steps in Configuration Manager

 *Applies to: System Center Configuration Manager (Current Branch)*

 The following task sequence steps can be added to a Configuration Manager task sequence. For information about editing a task sequence, see [Edit a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ModifyTaskSequence).  

 The following settings are common to all task sequence steps:

#### Properties tab
 - **Name**: The task sequence editor requires that you specify a short name to describe this step. When you add a new step, the task sequence editor sets the name to the Type by default. The **Name** length can't exceed 50 characters.  

 - **Description**: Optionally, specify more detailed information about this step. The **Description** length can't exceed 256 characters.  

 The rest of this article describes the other settings on the **Properties** tab for each task sequence step.

#### Options tab  

 - **Disable this step**: The task sequence skips this step when it runs on a computer. The icon for this step is greyed out in the task sequence editor.  

 - **Continue on error**: If an error occurs while running the step, the task sequence continues. For more information, see [Planning considerations for automating tasks](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#BKMK_TSGroups).   

 - **Add Condition**: The task sequence evaluates these conditional statements to determine if it runs the step. For an example of using a task sequence variable as a condition, see [How to use task sequence variables](/sccm/osd/understand/using-task-sequence-variables #bkmk_access-condition).   

 The sections below for specific task sequence steps describe other possible settings on the **Options** tab.



##  <a name="BKMK_ApplyDataImage"></a> Apply Data Image   

 Use this step to copy the data image to the specified destination partition.  

 This step runs only in Windows PE. It doesn't run in the full OS. 

 Use the following task sequence variables with this step:
 - [OSDDataImageIndex](/sccm/osd/understand/task-sequence-variables#OSDDataImageIndex)
 - [OSDWipeDestinationPartition](/sccm/osd/understand/task-sequence-variables#OSDWipeDestinationPartition)

 To add this step in the task sequence editor, click **Add**, select **Images**, and select **Apply Data Image**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Image Package  
 Click **Browse** to specify the **Image Package** used by this task sequence. Select the package you want to install in the **Select a Package** dialog box. The bottom of the dialog box displays the associated property information for each existing image package. Use the drop-down list to select the **Image** you want to install from the selected **Image Package**.  

 > [!NOTE]  
 >  This task sequence action treats the image as a data file. This action doesn't do any setup to boot the image as an OS.  

#### Destination  
 Configure one of the following options:

 - **Next available partition**: Use the next sequential partition that an **Apply Operating System** or **Apply Data Image** step in this task sequence has not already targeted.  

 - **Specific disk and partition**: Select the **Disk** number (starting with 0) and the **Partition** number (starting with 1).  

 - **Specific logical drive letter**: Specify the **Drive Letter** that Windows PE assigns to the partition. This drive letter can be different from the drive letter assigned by the newly deployed OS.  

 - **Logical drive letter stored in a variable**: Specify the task sequence variable that contains the drive letter assigned to the partition by Windows PE. This variable is typically set in the Advanced section of the **Partition Properties** dialog box for the **Format and Partition Disk** task sequence step.  

#### Delete all content on the partition before applying the image  
 Specifies that the task sequence deletes all files on the target partition before installing the image. By not deleting the content of the partition, this action can be used to apply additional content to a previously targeted partition.  



##  <a name="BKMK_ApplyDriverPackage"></a> Apply Driver Package  

 Use this step to download all of the drivers in the driver package and install them on the Windows OS.

 The **Apply Driver Package** task sequence step makes all device drivers in a driver package available for use by Windows. Add this step between the **Apply Operating System** and **Setup Windows and ConfigMgr** steps to make the drivers in the package available to Windows. Typically, the **Apply Driver Package** step is placed after the **Auto Apply Drivers** task sequence step. The **Apply Driver Package** task sequence step is also useful with stand-alone media deployment scenarios.  

 Put similar device drivers into a driver package, and distribute them to the appropriate distribution points. For example, put all drivers from one manufacturer into a driver package. Then distribute the package to distribution points where the associated computers can access them.

 The **Apply Driver Package** step is useful for stand-alone media. This step is also useful to install a specific set of drivers. These types of drivers include devices that Windows plug-and-play doesn't detect, such as network printers.  

 This task sequence step runs only in Windows PE. It doesn't run in the full OS. 

 Use the following task sequence variables with this step:
 - [OSDApplyDriverBootCriticalContentUniqueID](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalContentUniqueID)
 - [OSDApplyDriverBootCriticalHardwareComponent](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalHardwareComponent)
 - [OSDApplyDriverBootCriticalID](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalID)
 - [OSDApplyDriverBootCriticalINFFile](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalINFFile)
 - [OSDInstallDriversAdditionalOptions](/sccm/osd/understand/task-sequence-variables#OSDInstallDriversAdditionalOptions)<!--516679/2840016--> (starting in version 1806)

 To add this step in the task sequence editor, click **Add**, select **Drivers**, and select **Apply Driver Package**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Driver package
 Specify the driver package that contains the needed device drivers. Click **Browse** to launch the **Select a Package** dialog box. Select an existing driver package to apply. The bottom of the dialog box displays the associated package properties.  

#### Select the mass storage driver within the package that needs to be installed before setup on pre-Windows Vista operating systems
 Specify any mass storage drivers needed to install a classic OS.  

#### Driver
 Select the mass storage driver file to install before setup of a classic OS. The drop-down list populates from the specified package.  

#### Model  
 Specify the boot-critical device that is needed for pre-Windows Vista OS deployments.  

#### Do unattended installation of unsigned drivers on version of Windows where this is allowed**  
 This option allows Windows to install drivers without a digital signature.  



##  <a name="BKMK_ApplyNetworkSettings"></a> Apply Network Settings   

 Use this step to specify the network or workgroup configuration information for the destination computer. The task sequence stores these values in the appropriate answer file. Windows Setup uses this answer file during the **Setup Windows and ConfigMgr** action.  

 This task sequence step runs in either the full OS or Windows PE. 

 Use the following task sequence variables with this step:
 - [OSDAdapter](/sccm/osd/understand/task-sequence-variables#OSDAdapter)
 - [OSDAdapterCount](/sccm/osd/understand/task-sequence-variables#OSDAdapterCount)
 - [OSDDNSDomain](/sccm/osd/understand/task-sequence-variables#OSDDNSDomain)
 - [OSDDNSSuffixSearchOrder](/sccm/osd/understand/task-sequence-variables#OSDDNSSuffixSearchOrder)
 - [OSDDomainName](/sccm/osd/understand/task-sequence-variables#OSDDomainName)
 - [OSDDomainOUName](/sccm/osd/understand/task-sequence-variables#OSDDomainOUName)
 - [OSDEnableTCPIPFiltering](/sccm/osd/understand/task-sequence-variables#OSDEnableTCPIPFiltering)
 - [OSDJoinAccount](/sccm/osd/understand/task-sequence-variables#OSDJoinAccount)
 - [OSDJoinPassword](/sccm/osd/understand/task-sequence-variables#OSDJoinPassword)
 - [OSDWorkgroupName](/sccm/osd/understand/task-sequence-variables#OSDWorkgroupName)

 To add this step in the task sequence editor, click **Add**, select **Settings**, and select **Apply Network Settings**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Join a workgroup
 Select this option to have the destination computer join the specified workgroup. Enter the name of the workgroup on the **Workgroup** line. The value that the **Capture Network Settings** task sequence step captures can override this value. 

#### Join a domain
 Select this option to have the destination computer join the specified domain. Specify or browse to the domain, such as `fabricam.com`. Specify or browse to a Lightweight Directory Access Protocol (LDAP) path for an organizational unit. For example: `LDAP//OU=computers, DC=Fabricam.com, C=com`.  

#### Account
 Click **Set** to specify an account with the necessary permissions to join the computer to the domain. In the **Windows User Account** dialog box, enter the user name in the following format: `Domain\User`. For more information, see [Domain joining account](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account). 

#### Adapter settings  
 Specify network configurations for each network adapter in the computer. Click **New** to open the **Network Settings** dialog box, and then specify the network settings. 
 - If you also use the **Capture Network Settings** step, the task sequence applies the previously captured settings to the network adapter. 
 - If the task sequence didn't previously capture network settings, it applies the settings you specify in this step. 
 - The task sequence applies these settings to network adapters in Windows device enumeration order.  
 - The task sequence doesn't immediately apply the settings you specify in this step to the computer. 



##  <a name="BKMK_ApplyOperatingSystemImage"></a> Apply Operating System Image  

 > [!TIP]  
 > Beginning with Windows 10, version 1709, media includes multiple editions. When you configure a task sequence to use an OS upgrade package or OS image, be sure to select a [supported edition](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).  

 Use this step to install an OS on the destination computer. 

 > [!NOTE]  
 >  The **Setup Windows and ConfigMgr** step starts the installation of Windows. 

 After the **Apply Operating System** action runs, it sets the **OSDTargetSystemDrive** variable to the drive letter of the partition containing the OS files.  

 This task sequence step runs only in Windows PE. It doesn't run in the full OS. 

 Use the following task sequence variables with this step:
 - [OSDConfigFileName](/sccm/osd/understand/task-sequence-variables#OSDConfigFileName)
 - [OSDImageIndex](/sccm/osd/understand/task-sequence-variables#OSDImageIndex)
 - [OSDTargetSystemDrive](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemDrive)

 To add this step in the task sequence editor, click **Add**, select **Images**, and select **Apply Operating System Image**. 

 This step performs actions depending on whether it uses an OS image or an OS upgrade package.  

 #### OS image actions
 The **Apply Operating System Image** step performs the following actions when using an OS image:  

 1.  Delete all content on the targeted volume, except files in the folder specified by the **\_SMSTSUserStatePath** variable.  

 2.  Extract the contents of the specified .wim file to the specified destination partition.  

 3.  Prepare the answer file:  

    1.  Create a new default Windows Setup answer file (sysprep.inf or unattend.xml) for the deployed OS.  

    2.  Merge any values from the user-supplied answer file.  

 4.  Copy Windows boot loaders into the active partition.  

 5.  Set the boot.ini or the Boot Configuration Database (BCD) to reference the newly installed OS.  

#### OS upgrade package actions
 The **Apply Operating System Image** step performs the following actions when using an OS upgrade package:  

 1.  Delete all content on the targeted volume, except files in the folder specified by the **\_SMSTSUserStatePath** variable.  

 2.  Prepare the answer file:  

    1.  Create a fresh answer file with standard values created by Configuration Manager.  

    2.  Merge any values from the user-supplied answer file.  


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Apply operating system from a captured image
 Installs an OS image that you captured. Click **Browse** to open the **Select a package** dialog box. Then select the existing image package you want to install. If multiple images are associated with the specified **Image package**, select from the drop-down list the associated image to use for this deployment. You can view basic information about each existing image by clicking on it.  

#### Apply operating system image from an original installation source
 Installs an OS using an OS upgrade package, which is also an original installation source. Click **Browse** to open the **Select and Operating System Install Package** dialog box. Then select the existing OS upgrade package you want to use. You can view basic information about each existing image source by clicking on it. The results pane at the bottom of the dialog box displays the associated image source properties. If there are multiple editions associated with the specified package, use the drop-down list to select the **Edition** you want to use.  

#### Use an unattended or sysprep answer file for a custom installation
 Use this option to provide a Windows setup answer file (**unattend.xml**, **unattend.txt**, or **sysprep.inf**) depending on the OS version and installation method. The file you specify can include any of the standard configuration options supported by Windows answer files. For example, you can use it to specify the default Internet Explorer home page. Specify the package that contains the answer file and the associated path to the file in the package.  

 > [!NOTE]  
 >  The Windows setup answer file that you supply can contain embedded task sequence variables of the form `%varname%`, where *varname* is the name of the variable. The **Setup Windows and ConfigMgr** step substitutes the variable string for the actual value of the variable. You can't use these embedded task sequence variables in numeric-only fields in an unattend.xml answer file.  

 If you don't supply a Windows setup answer file, the task sequence automatically generates an answer file.  

#### Destination  
 Configure one of the following options:  

 - **Next available partition**: Use the next sequential partition not already targeted by an **Apply Operating System** or **Apply Data Image** step in this task sequence.  

 - **Specific disk and partition**: Select the **Disk** number (starting with 0) and the **Partition** number (starting with 1).  

 - **Specific logical drive letter**: Specify the **Drive Letter** assigned to the partition by Windows PE. This drive letter can be different from the drive letter assigned by the newly deployed OS.  

 - **Logical drive letter stored in a variable**: Specify the task sequence variable containing the drive letter assigned to the partition by Windows PE. This variable is typically set in the Advanced section of the **Partition Properties** dialog box for the **Format and Partition Disk** task sequence step.  


### Options  

 Besides the default options, configure the following additional settings on the **Options** tab of this task sequence step:  

#### Access content directly from the distribution point
 Configure the task sequence to access the OS image directly from the distribution point. For example, use this option when you deploy operating systems to embedded devices that have limited storage capacity. When selecting this option, also configure the package share settings on the **Data Access** tab of the OS image properties.  

 > [!NOTE]  
 >  This setting overrides the deployment option that you configure on the **Distribution Points** page in the **Deploy Software Wizard**. This override is only for the OS image that this step specifies, not for all task sequence content.  



##  <a name="BKMK_ApplyWindowsSettings"></a> Apply Windows Settings  

 Use this step to configure the Windows settings for the destination computer. The task sequence stores these values in the appropriate answer file. Windows Setup uses this answer file during the **Setup Windows and ConfigMgr** step.  

 This task sequence step runs only in Windows PE. It doesn't run in the full OS.  

 Use the following task sequence variables with this step:
 - [OSDComputerName](/sccm/osd/understand/task-sequence-variables#OSDComputerName-input)
 - [OSDLocalAdminPassword](/sccm/osd/understand/task-sequence-variables#OSDLocalAdminPassword)
 - [OSDProductKey](/sccm/osd/understand/task-sequence-variables#OSDProductKey)
 - [OSDRandomAdminPassword](/sccm/osd/understand/task-sequence-variables#OSDRandomAdminPassword)
 - [OSDRegisteredOrgName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredOrgName-input)
 - [OSDRegisteredUserName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredUserName)
 - [OSDServerLicenseConnectionLimit](/sccm/osd/understand/task-sequence-variables#OSDServerLicenseConnectionLimit)
 - [OSDServerLicenseMode](/sccm/osd/understand/task-sequence-variables#OSDServerLicenseMode)
 - [OSDTimeZone](/sccm/osd/understand/task-sequence-variables#OSDTimeZone-input)

 To add this step in the task sequence editor, click **Add**, select **Settings**, and select **Apply Windows Settings**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### User name
 Specify the registered user name to associate with the destination computer. The value that the **Capture Windows Settings** task sequence step captures can override this value.  

#### Organization name
 Specify the registered organization name to associate with the destination computer. The value that the **Capture Windows Settings** task sequence step captures can override this value.  

#### Product key  
 Specify the product key to use for the Windows installation on the destination computer.  

#### Server licensing  
 Specify the server licensing mode. 
 - Select **Per server** or **Per user** as the licensing mode.  
 - If you select **Per server**, also specify the maximum number of connections permitted per your license agreement.  
 - If the destination computer isn't a server, or you don't want to specify the licensing mode, select **Do not specify**.   

#### Maximum connections
 Specify the maximum number of connections that are available for this computer as stated in your license agreement.  

#### Randomly generate the local administrator password and disable the account on all supported platforms (recommended)  
 Select this option to set the local administrator password to a randomly generated string. This option also disables the local administrator account on platforms that support this capability.  

#### Enable the account and specify the local administrator password  
 Select this option to enable the local administrator account using the specified password. Enter the password on the **Password** line and confirm the password on the **Confirm password** line.  

#### Time Zone
 Specify the time zone to configure on the destination computer. The value that the **Capture Windows Settings** task sequence step captures can override this value.  



##  <a name="BKMK_AutoApplyDrivers"></a> Auto Apply Drivers  

 Use this step to match and install drivers as part of the OS deployment.  

 The **Auto Apply Drivers** task sequence step performs the following actions:  

 1. Scan the hardware and find the plug-and-play IDs for all devices present on the system.  

 2. Send the list of devices and their plug-and-play IDs to the management point. The management point returns a list of compatible drivers from the driver catalog for each hardware device. The list includes all enabled drivers regardless of what driver package they are in, and drivers tagged with the specified driver category.  

 3. For each hardware device, the task sequence picks the best driver. This driver is appropriate for the deployed OS, and is on an accessible distribution point.  

 4. The task sequence downloads the selected drivers from a distribution point, and stages the drivers on the target OS.  

    1. When using an OS image, the task sequence places the drivers into the OS driver store.  

    2. When using an OS upgrade package as an original installation source, the task sequence configures Windows Setup with the drivers' location.  

 5.  During the **Setup Windows and ConfigMgr** step in the task sequence, Windows Setup finds the drivers staged by this step.  

 > [!IMPORTANT]  
 >  Stand-alone media can't use the **Auto Apply Drivers** step. The task sequence has no connection to the Configuration Manager site in this scenario.  

 This task sequence step runs only in Windows PE. It doesn't run in the full OS.

 Use the following task sequence variables with this step:
 - [OSDAutoApplyDriverBestMatch](/sccm/osd/understand/task-sequence-variables#OSDAutoApplyDriverBestMatch)
 - [OSDAutoApplyDriverCategoryList](/sccm/osd/understand/task-sequence-variables#OSDAutoApplyDriverCategoryList)
 - [SMSTSDriverRequestConnectTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestConnectTimeOut)
 - [SMSTSDriverRequestReceiveTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestReceiveTimeOut)
 - [SMSTSDriverRequestResolveTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestResolveTimeOut)
 - [SMSTSDriverRequestSendTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestSendTimeOut)

 To add this step in the task sequence editor, click **Add**, select **Drivers**, and select **Auto Apply Drivers**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Install only the best matched compatible drivers
 Specifies that the task sequence step installs only the best matched driver for each hardware device detected.  

#### Install all compatible drivers
 The task sequence installs all drivers compatible for each detected hardware device. Windows Setup then chooses the best driver. This option takes more network bandwidth and disk space. The task sequence downloads more drivers, but Windows can select a better driver.  

#### Consider drivers from all categories
 The task sequence searches all available driver categories for the appropriate device drivers.  

#### Limit driver matching to only consider drivers in selected categories
 The task sequence searches in the specified driver categories for the appropriate device drivers.  

#### Do unattended installation of unsigned drivers on versions of Windows where this is allowed
 This option allows Windows to install drivers without a digital signature.   

 > [!IMPORTANT]  
 >  This option doesn't apply to operating systems where you can't configure driver signing policy.  



##  <a name="BKMK_CaptureNetworkSettings"></a> Capture Network Settings  

 Use this step to capture Microsoft network settings from the computer running the task sequence. The task sequence saves these settings in task sequence variables. These settings override the default settings you configure on the **Apply Network Settings** step.  

 This task sequence step runs only in the full OS. It doesn't run in Windows PE.  

 Use the following task sequence variables with this step:
 - [OSDMigrateAdapterSettings](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdapterSettings)
 - [OSDMigrateNetworkMembership](/sccm/osd/understand/task-sequence-variables#OSDMigrateNetworkMembership)

 To add this step in the task sequence editor, click **Add**, select **Settings**, and select **Capture Network Settings**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Migrate domain and workgroup membership 
 Captures the domain and workgroup membership information of the destination computer.  

#### Migrate network adapter configuration
 Captures the network adapter configuration of the destination computer. It captures the following information: 
 - Global network settings  
 - Number of adapters  
 - The following network settings associated with each adapter: DNS, WINS, IP, and port filters



##  <a name="BKMK_CaptureOperatingSystemImage"></a> Capture Operating System Image  

 This step captures one or more images from a reference computer. The task sequence creates a Windows image (.wim) file on the specified network share. Then use the **Add Operating System Image Package** wizard to import this image into Configuration Manager for image-based OS deployments.  

 Configuration Manager captures each volume (drive) from the reference computer to a separate image within the .wim file. If the referenced computer has multiple volumes, the resulting .wim file contains a separate image for each volume. This step only captures volumes that are formatted as NTFS or FAT32. It skips volumes with other formats, and USB volumes.  

 The installed OS on the reference computer must be a version of Windows that Configuration Manager supports. Use the SysPrep tool to prepare the OS on the reference computer. The installed OS volume and the boot volume must be the same volume.  

 Specify an account with write permissions to the selected network share. For more information on the capture OS image account, see [Accounts](/sccm/core/plan-design/hierarchy/accounts#capture-operating-system-image-account).

 This task sequence step runs only in Windows PE. It doesn't run in the full OS. 

 Use the following task sequence variables with this step:
 - [OSDCaptureAccount](/sccm/osd/understand/task-sequence-variables#OSDCaptureAccount)
 - [OSDCaptureAccountPassword](/sccm/osd/understand/task-sequence-variables#OSDCaptureAccountPassword)
 - [OSDCaptureDestination](/sccm/osd/understand/task-sequence-variables#OSDCaptureDestination)
 - [OSDImageCreator](/sccm/osd/understand/task-sequence-variables#OSDImageCreator)
 - [OSDImageDescription](/sccm/osd/understand/task-sequence-variables#OSDImageDescription)
 - [OSDImageVersion](/sccm/osd/understand/task-sequence-variables#OSDImageVersion)
 - [OSDTargetSystemRoot](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemRoot-input)

 To add this step in the task sequence editor, click **Add**, select **Images**, and select **Capture Operating System Image**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Target  
 File system path to the location that Configuration Manager uses when storing the captured OS image.  

#### Description  
 An optional user-defined description of the captured OS image that's stored in the image file.  

#### Version  
 An optional user-defined version number to assign to the captured OS image. This value can be any combination of letters and numbers. It's stored in the image file.  

#### Created by  
 The optional name of the user that created the OS image. It's stored in the image file.  

#### Capture operating system image account  
 Enter the Windows account that has permissions to the specified network share. Click **Set** to specify the name of the Windows account.  



##  <a name="BKMK_CaptureUserState"></a> Capture User State  

 This step uses the User State Migration Tool (USMT) to capture user state and settings from the computer running the task sequence. This task sequence step is used in conjunction with the **Restore User State** task sequence step. This step always encrypts the USMT state store by using an encryption key that Configuration Manager generates and manages.  

 For more information about managing the user state when deploying operating systems, see [Manage user state](/sccm/osd/get-started/manage-user-state).  

 If you want to save and restore user state settings from a state migration point, use this step with the **Request State Store** and **Release State Store** steps.  

 This step provides control over a limited subset of the most commonly used USMT options. Specify additional command-line options using the **OSDMigrateAdditionalCaptureOptions** task sequence variable.  

 This task sequence step runs only in Windows PE. It doesn't run in the full OS.   

 Use the following task sequence variables with this step:
 - [_OSDMigrateUsmtPackageID](/sccm/osd/understand/task-sequence-variables#OSDMigrateUsmtPackageID)
 - [OSDMigrateAdditionalCaptureOptions](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdditionalCaptureOptions)
 - [OSDMigrateConfigFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateConfigFiles)
 - [OSDMigrateContinueOnLockedFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateContinueOnLockedFiles)
 - [OSDMigrateEnableVerboseLogging](/sccm/osd/understand/task-sequence-variables#OSDMigrateEnableVerboseLogging)
 - [OSDMigrateMode](/sccm/osd/understand/task-sequence-variables#OSDMigrateMode)
 - [OSDMigrateSkipEncryptedFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateSkipEncryptedFiles)
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)

 To add this step in the task sequence editor, click **Add**, select **User State**, and select **Capture User State**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### User state migration tool package
 Specify the package that contains the User State Migration Tool (USMT). The task sequence uses this version of USMT to capture the user state and settings. This package doesn't require a program. Specify a package containing the 32-bit or 64-bit version of USMT. The architecture of USMT depends upon the architecture of the OS from which the task sequence is capturing state.  

#### Capture all user profiles with standard options
 Migrate all user profile information. This option is the default.  

 If you select this option, but don't select **Restore local computer user profiles** in the **Restore User State** step, the task sequence fails. Configuration Manager can't migrate the new accounts without assigning them passwords. 

 When you use the **Install an existing image package** option of the **New Task Sequence** wizard, the resulting task sequence defaults to **Capture all user profiles with standard options**. This default task sequence doesn't select the option to **Restore local computer user profiles**, or non-domain user accounts.  

 Select **Restore local computer user profiles** and provide a password for the account to migrate. In a manually created task sequence, this setting is found under the **Restore User State** step. In a task sequence created by the **New Task Sequence** wizard, this setting is found under the step **Restore User Files and Settings** wizard page.  

 If you have no local user accounts, this setting doesn't apply.  

#### Customize how user profiles are captured
 Select this option to specify a custom profile file for migration. Click **Files** to select the configuration files for USMT to use with this step. Specify a custom .xml file that contains rules that define the user state files to migrate.  

#### Click here to select configuration files
 Select this option to select the configuration files in the USMT package you want to use for capturing user profiles. Click the **Files** button to launch the **Configuration Files** dialog box. To specify a configuration file, enter the name of the file on the **Filename** line and click the **Add** button.  

#### Enable verbose logging
 Enable this option to generate more detailed log file information. When capturing state, the task sequence by default generates **ScanState.log** in the task sequence log folder, `%WinDir%\ccm\logs`.   

#### Skip files using encrypted file system
 Enable this option to skip capturing files encrypted with the Encrypted File System (EFS). These files include user profile files. Depending on the OS and USMT versions, encrypted files might not be readable after you restore. For more information, see the USMT documentation.  

#### Copy by using file system access
 Enable this option to specify any of the following settings:  

 - **Continue if some files cannot be captured**: Enable this setting to continue the migration process even if it can't capture some files. If you disable this option, and a file can't be captured, then this step fails. This option is enabled by default.  

 - **Capture locally by using links instead of by copying files**: Enable this setting to use NTFS hard-links to capture files.  

     For more information about migrating data using hard-links, see [Hard-Link Migration Store](https://docs.microsoft.com/windows/deployment/usmt/usmt-hard-link-migration-store).  

 - **Capture in off-line mode (Windows PE only)**: Enable this setting to capture the user state while in Windows PE instead of the full OS.  

#### Capture by using Volume Copy Shadow Services (VSS)
 This option allows you to capture files even if they're locked for editing by another application.  



##  <a name="BKMK_CaptureWindowsSettings"></a> Capture Windows Settings  

 Use this step to capture the Windows settings from the computer running the task sequence. The task sequence saves these settings in task sequence variables. These captured settings override the default settings that you configure on the **Apply Windows Settings** step.  

 This task sequence step runs in either Windows PE or the full OS.  

 Use the following task sequence variables with this step:
 - [OSDComputerName](/sccm/osd/understand/task-sequence-variables#OSDComputerName-output)
 - [OSDMigrateComputerName](/sccm/osd/understand/task-sequence-variables#OSDMigrateComputerName)
 - [OSDMigrateRegistrationInfo](/sccm/osd/understand/task-sequence-variables#OSDMigrateRegistrationInfo)
 - [OSDMigrateTimeZone](/sccm/osd/understand/task-sequence-variables#OSDMigrateTimeZone)
 - [OSDRegisteredOrgName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredOrgName-output)
 - [OSDTimeZone](/sccm/osd/understand/task-sequence-variables#OSDTimeZone-output)

 To add this step in the task sequence editor, click **Add**, select **Settings**, and select **Capture Windows Settings**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Migrate computer name
 Capture the NetBIOS computer name of the computer.  

#### Migrate registered user and organization names
 Capture the registered user and organization names from the computer.  

#### Migrate time zone
 Capture the time zone setting on the computer.  



##  <a name="BKMK_CheckReadiness"></a> Check Readiness  

 Use this step to verify that the target computer meets the specified deployment prerequisite conditions.  

 To add this step in the task sequence editor, click **Add**, select **General**, and select **Check Readiness**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Ensure minimum memory (MB)
 Verify that the amount of memory, in megabytes (MB), meets or exceeds the specified amount. The step enables this setting by default.  

#### Ensure minimum processor speed (MHz)  
 Verify that the speed of the processor, in megahertz (MHz), meets or exceeds the specified amount. The step enables this setting by default.  

#### Ensure minimum free disk space (MB)
 Verify that the amount of free disk space, in megabytes (MB), meets or exceeds the specified amount.  

#### Ensure current OS to be refreshed is
 Verify that the OS installed on the target computer meets the specified requirement. The step sets this setting to **CLIENT** by default.  


### Options

 > [!NOTE]  
 > If you enable the **Continue on error** setting on the **Options** tab of this step, it only logs the readiness check results. If a check fails, the task sequence doesn't stop.  



##  <a name="BKMK_ConnectToNetworkFolder"></a> Connect To Network Folder  

 Use this step to create a connection to a shared network folder.  

 This task sequence step runs in the full OS or Windows PE.  

 Use the following task sequence variables with this step:
 - [SMSConnectNetworkFolderAccount](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderAccount)
 - [SMSConnectNetworkFolderDriveLetter](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderDriveLetter)
 - [SMSConnectNetworkFolderPassword](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderPassword)
 - [SMSConnectNetworkFolderPath](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderPath)

 To add this step in the task sequence editor, click **Add**, select **General**, and select **Connect To Network Folder**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Path  
 Click **Browse** to specify the network folder path. Use the format `\\server\share`.

#### Drive  
 Select the local drive letter to assign for this connection. 

#### Account 
 Click **Set** to specify the user account with permissions to connect to this network folder. For more information on the task sequence network folder connection account, see [Accounts](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-network-folder-connection-account).



##  <a name="BKMK_DisableBitLocker"></a> Disable BitLocker  

 Use this step to disable BitLocker encryption on the current OS drive, or on a specific drive. This action leaves the key protectors visible in clear text on the hard drive. It doesn't decrypt the contents of the drive. This action completes almost instantly.  

 > [!NOTE]  
 >  BitLocker drive encryption provides low-level encryption of the contents of a disk volume.  

 If you have multiple encrypted drives, disable BitLocker on any data drives before disabling BitLocker on the OS drive.  

 This step runs only in the full OS. It doesn't run in Windows PE.  

 To add this step in the task sequence editor, click **Add**, select **Disks**, and select **Disable BitLocker**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Current operating system drive
 Disables BitLocker on the current OS drive.  

#### Specific drive  
 Disables BitLocker on a specific drive. Use the drop-down list to specify the drive where BitLocker is disabled.  



##  <a name="BKMK_DownloadPackageContent"></a> Download Package Content  

 Use this step to download any of the following package types:  

 - OS images  
 - OS upgrade packages  
 - Driver packages  
 - Packages  
 - Boot images  

 This step works well in a task sequence to upgrade an OS in the following scenarios:  

 - To use a single upgrade task sequence that can work with both x86 and x64 platforms. Include two **Download Package Content** steps in the **Prepare for Upgrade** group. Specify conditions on the **Options** tab to detect the client architecture, and download only the appropriate OS upgrade package. Configure each **Download Package Content** step to use the same variable. Use the variable for the media path on the **Upgrade Operating System** step.  

 - To dynamically download an applicable driver package, use two **Download Package Content** steps with conditions to detect the appropriate hardware type for each driver package. Configure each **Download Package Content** step to use the same variable. Use the variable for the **Staged content** value in the Drivers section of the **Upgrade Operating System** step.  

 > [!NOTE]    
 > When you deploy a task sequence that contains this step, don't select **Download all content locally before starting the task sequence** or **Access content directly from a distribution point** for **Deployment options** on the **Distribution Points** page of the Deploy Software Wizard.  

 This step runs in either the full OS or Windows PE. The option to save the package in the Configuration Manager client cache isn't supported in Windows PE.

 To add this step in the task sequence editor, click **Add**, select **Software**, and select **Download Package Content**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Select package  
 Click the icon to select the package to download. After you select one package, click the icon again to choose another package.  

#### Place into the following location
 Choose to save the package in one of the following locations:  

 - **Task sequence working directory**: This location is also referred to as the task sequence cache.  

 - **Configuration Manager client cache**: Use this option to store the content in the client cache. By default, this path is `%WinDir%\ccmcache`.  

 - **Custom path**: The task sequence engine first downloads the package to the task sequence working directory. It then moves the content to this path you specify. The task sequence engine appends the path with the package ID.  

#### Save path as a variable
 Save the package's path into a custom task sequence variable. Then use this variable in another task sequence step. 

 Configuration Manager adds a numerical suffix to the variable name. For example, you specify a variable of `%MyContent%` as a custom variable. It's the root for where the task sequence stores all referenced content for this step. This content may contain multiple packages. When you refer to the variable, add a numerical suffix. For the first package, refer to `%MyContent01%`. When you refer to the variable in subsequent steps, such as **Upgrade Operating System**, use `%MyContent02%` or `%MyContent03%`, where the number corresponds to the order that the **Download Package Content** step lists the packages.  

#### If a package download fails, continue downloading other packages in the list
 If the task sequence fails to download a package, it starts to download the next package in the list.  



##  <a name="BKMK_EnableBitLocker"></a> Enable BitLocker  

 Use this step to enable BitLocker encryption on at least two partitions on the hard drive. The first active partition contains the Windows bootstrap code. Another partition contains the OS. The bootstrap partition must remain unencrypted.  

 Use the **Pre-provision BitLocker** step to enable BitLocker on a drive while in Windows PE. For more information, see [Pre-provision BitLocker](#BKMK_PreProvisionBitLocker).  

 > [!NOTE]  
 >  BitLocker drive encryption provides low-level encryption of the contents of a disk volume.  

 This step runs only in the full OS. It doesn't run in Windows PE.   

 Use the following task sequence variables with this step:
 - [OSDBitLockerRecoveryPassword](/sccm/osd/understand/task-sequence-variables#OSDBitLockerRecoveryPassword)
 - [OSDBitLockerStartupKey](/sccm/osd/understand/task-sequence-variables#OSDBitLockerStartupKey)

 When you specify **TPM Only**, **TPM and Startup Key on USB**, or **TPM and PIN**, the Trusted Platform Module (TPM) must be in the following state before you can run the **Enable BitLocker** step:  
 - Enabled  
 - Activated  
 - Ownership Allowed  

 This step completes any remaining TPM initialization. The remaining steps don't require physical presence or reboots. The **Enable BitLocker** step transparently completes the following remaining TPM initialization steps, if necessary:  
 - Create endorsement key pair  
 - Create owner authorization value and escrow to Active Directory, which must have been extended to support this value  
 - Take ownership  
 - Create the storage root key, or reset if already present but incompatible  
   
 If you want the task sequence to wait for the **Enable BitLocker** step to complete the drive encryption process, then select the **Wait** option. If you don't select the **Wait** option, the drive encryption process happens in the background. The task sequence immediately proceeds to the next step.  

 BitLocker can be used to encrypt multiple drives on a computer system, both OS and data drives. To encrypt a data drive, first encrypt the OS drive and complete the encryption process. This requirement is because the OS drive stores the key protectors for the data drives. If you encrypt the OS and data drives in the same task sequence, select the **Wait** option on the **Enable BitLocker** step for the OS drive.  

 If the hard drive is already encrypted, but BitLocker is disabled, then the **Enable BitLocker** step re-enables the key protectors and completes quickly. Re-encryption of the hard drive isn't necessary in this case.  

 To add this step in the task sequence editor, click **Add**, select **Disks**, and select **Enable BitLocker**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Choose the drive to encrypt
 Specifies the drive to encrypt. To encrypt the current OS drive, select **Current operating system drive**. Then configure one of the following options for key management:  

 - **TPM only**: Select this option to use only Trusted Platform Module (TPM).  

 - **Startup Key on USB only**: Select this option to use a startup key stored on a USB flash drive. When you select this option, BitLocker locks the normal boot process until a USB device that contains a BitLocker startup key is attached to the computer.  

 - **TPM and Startup Key on USB**: Select this option to use TPM and a startup key stored on a USB flash drive. When you select this option, BitLocker locks the normal boot process until a USB device that contains a BitLocker startup key is attached to the computer.  

 - **TPM and PIN**: Select this option to use TPM and a personal identification number (PIN). When you select this option, BitLocker locks the normal boot process until the user provides the PIN.  

 To encrypt a specific, non-OS data drive, select **Specific drive**. Then select the drive from the list.  

#### Choose where to create the recovery key
 To specify for BitLocker to create the recovery password and escrow it in Active Directory, select **In Active Directory**. This option requires that you extend Active Directory for BitLocker key escrow. BitLocker can then save the associated recovery information in Active Directory. Select **Do not create recovery key** to not create a password. Creating a password is the recommended option.  

#### Wait for BitLocker to complete the drive encryption process on all drives before continuing task sequence execution
 Select this option to allow BitLocker drive encryption to complete prior to running the next step in the task sequence. If you select this option, BitLocker encrypts the entire disk volume before the user is able to sign in to the computer.  

 The encryption process can take hours to complete when encrypting a large hard drive. Not selecting this option allows the task sequence to proceed immediately.  



##  <a name="BKMK_FormatandPartitionDisk"></a> Format and Partition Disk  

 Use this step to format and partition a specified disk on the destination computer.  

 > [!IMPORTANT]  
 >  Every setting you specify for this step applies to a single specified disk. To format and partition another disk on the destination computer, add an additional **Format and Partition Disk** step to the task sequence.  

 This step runs only in Windows PE. It doesn't run in the full OS.  

 Use the following task sequence variables with this step:
 - [OSDDiskIndex](/sccm/osd/understand/task-sequence-variables#OSDDiskIndex)
 - [OSDGPTBootDisk](/sccm/osd/understand/task-sequence-variables#OSDGPTBootDisk)
 - [OSDPartitions](/sccm/osd/understand/task-sequence-variables#OSDPartitions)
 - [OSDPartitionStyle](/sccm/osd/understand/task-sequence-variables#OSDPartitionStyle)

 To add this step in the task sequence editor, click **Add**, select **Disks**, and select **Format and Partition Disk**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Disk Number
 The physical disk number of the disk to format. The number is based on Windows disk enumeration ordering.  

#### Disk Type
 The type of the disk to format. There are two options to select from the drop-down list: 
 - **Standard (MBR)**: Master Boot Record  
 - **GPT**: GUID Partition Table  

 > [!NOTE]  
 >  If you change the disk type from **Standard (MBR)** to **GPT**, and the partition layout contains an extended partition, the task sequence removes all extended and logical partitions from the layout. The task sequence editor prompts to confirm this action before changing the disk type.  
   
#### Volume
 Specific information about the partition or volume that the task sequence creates, including the following attributes:  
 - Name  
 - Remaining disk space  

 To create a new partition, click **New** to launch the **Partition Properties** dialog box. Specify the partition type and size, and if it's a boot partition. To modify an existing partition, click the partition to be modified, and then click the **Properties** button. For more information about how to configure hard drive partitions, see one of the following articles:  

 - [UEFI/GPT-based hard drive partitions](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
 - [BIOS/MBR-based hard drive partitions](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  

 To delete a partition, select the partition, and then click **Delete**.  



##  <a name="BKMK_InstallApplication"></a> Install Application  

 This step installs the specified applications, or a set of applications defined by a dynamic list of task sequence variables. When the task sequence runs this step, the application installation begins immediately without waiting for a policy polling interval.  

 The applications must meet the following criteria:  

 - The application must have a deployment type of **Windows Installer** or **Script** installer. Windows app package (.appx file) deployment types aren't supported.  

 - It must run under the Local System account and not the user account.  

 - It must not interact with the desktop. The program must run silently or in an unattended mode.  

 - It must not initiate a restart on its own. The application must request a restart by using the standard restart code, 3010. This behavior makes sure that this step correctly handles the restart. If the application returns a 3010 exit code, the task sequence engine restarts the computer. After the restart, the task sequence automatically continues.  

 When this step runs, the application checks the applicability of the requirement rules and detection method on its deployment types. Based on the results of this check, the application installs the applicable deployment type. If a deployment type contains dependencies, the dependent deployment type is evaluated and installed as part of this step. Application dependencies aren't supported for stand-alone media.  

 > [!NOTE]  
 >  To install an application that supersedes another application, the content files for the superseded application must be available. Otherwise this task sequence step fails. For example, Microsoft Visio 2010 is installed on a client or in a captured image. When the **Install Application** step installs Microsoft Visio 2013, the content files for Microsoft Visio 2010 (the superseded application) must be available on a distribution point. If Microsoft Visio isn't installed at all on a client or captured image, the task sequence installs Microsoft Visio 2013 without checking for the Microsoft Visio 2010 content files.  

 > [!NOTE]  
 > If the client fails to retrieve the management point list from location services, use the **SMSTSMPListRequestTimeoutEnabled** and **SMSTSMPListRequestTimeout** task sequence variables. These variables specify how many milliseconds a task sequence waits before it retries installing an application. For more information, see [Task sequence variables](task-sequence-variables.md).

 This task sequence step runs only in the full OS. It doesn't run in Windows PE.  

 Use the following task sequence variables with this step:
 - [_TSAppInstallStatus](/sccm/osd/understand/task-sequence-variables#TSAppInstallStatus)
 - [SMSTSMPListRequestTimeoutEnabled](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeoutEnabled)
 - [SMSTSMPListRequestTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeout)
 - [TSErrorOnWarning](/sccm/osd/understand/task-sequence-variables#TSErrorOnWarning)

 To add this step in the task sequence editor, click **Add**, select **Software**, and select **Install Application**. 


### Properties  

 On the **Properties** tab for this step, configure the settings that are described in this section.  

#### Install the following applications
 The task sequence installs these applications in the specified order.  

 Configuration Manager filters out any disabled applications, or any applications with the following settings:  

 - Only when a user is logged on  
 - Run with user rights  

 These applications don't appear in the **Select the application to install** dialog box.

#### Install applications according to dynamic variable list
 The task sequence installs applications using this base variable name. The base variable name is for a set of task sequence variables defined for a collection or computer. These variables specify the applications that the task sequence installs for that collection or computer. Each variable name consists of its common base name plus a numerical suffix starting at 01. The value for each variable must contain the name of the application and nothing else.  

 For the task sequence to install applications by using a dynamic variable list, enable the following setting on the **General** tab of the application **Properties**: **Allow this application to be installed from the Install Application task sequence action instead of deploying manually**.  

 > [!NOTE]  
 >  You can't install applications by using a dynamic variable list for stand-alone media deployments.  

 For example, to install a single application by using a task sequence variable called AA01, specify the following variable:  

 |Variable Name|Variable Value|  
 |-------------------|--------------------|  
 |AA01|Microsoft Office|  

 To install two applications, specify the following variables:  

 |Variable Name|Variable Value|  
 |-------------------|--------------------|  
 |AA01|Microsoft Lync|  
 |AA02|Microsoft Office|  

 The following conditions affect the applications installed by the task sequence:  

 - If the value of a variable contains any information other than the name of the application. The task sequence doesn't install the application, and the task sequence continues.  

 - If the task sequence doesn't find a variable with the specified base name and "01" suffix, the task sequence doesn't install any applications.  

 > [!Important]  
 > These values are case-sensitive. For example, "install" is different than "Install". If you need to change the value, the task sequence editor doesn't detect a change of case. Make another edit at the same time, for example, modify the step description.<!--509714-->   

#### If an application fails, continue installing other applications in the list
 This setting specifies that the step continues when an individual application installation fails. If you specify this setting, the task sequence continues regardless of any installation errors. If you don't specify this setting, and the installation fails, the step immediately ends.  


### Options

 > [!NOTE]  
 > When you select **Continue on error** on the **Options** tab of this step, the task sequence continues when an application fails to install. When you don't enable this option, the task sequence fails, and doesn't install remaining applications.  

 Besides the default options, configure the following additional settings on the **Options** tab of this task sequence step:  

#### Retry this step if computer unexpectedly restarts
 If one of the application installations unexpectedly restarts the computer, retry this step. The step enables this setting by default with two retries. You can specify from one to five retries.  



##  <a name="BKMK_InstallPackage"></a> Install Package

 Use this step to install a software package as part of the task sequence. When this step runs, the installation begins immediately without waiting for a policy polling interval.  

 The package must meet the following criteria:  

 - It must run under the Local System account and not a user account.  

 - It shouldn't interact with the desktop. The program must run silently or in an unattended mode.  

 - It must not initiate a restart on its own. The software must request a restart using the standard restart code, 3010. This behavior makes sure that the task sequence properly handles the restart. If the software does return a 3010 exit code, the task sequence engine restarts the computer. After the restart, the task sequence automatically continues.  

 Programs that use the **Run another program first** option to install a dependent program aren't supported when deploying an OS. If you enable the package option **Run another program first**, and the dependent program already ran on the destination computer, the dependent program runs and the task sequence continues. However, if the dependent program hasn't already run on the destination computer, the task sequence step fails.  

 > [!NOTE]  
 >  The central administration site doesn't have the necessary client configuration policies required to enable the software distribution agent during the task sequence. When you create stand-alone media for a task sequence at the central administration site, and the task sequence includes an **Install Package** step, the following error might appear in the CreateTsMedia.log file:  
 >   
 >  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
 >   
 >  For stand-alone media that includes an **Install Package** step, create the stand-alone media at a primary site that has the software distribution agent enabled. Alternatively, add a **Run Command Line** step after the **Setup Windows and ConfigMgr** step and before the first **Install Package** step. The **Run Command Line** step runs a WMIC command to enable the software distribution agent before the first **Install Package** step. Use the following command in the **Run Command Line** step:  
 >   
 >  `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
 >   
 >  For more information about creating stand-alone media, see [Create stand-alone media](/sccm/osd/deploy-use/create-stand-alone-media).  

 This task sequence step runs only in the full OS. It doesn't run in Windows PE.  

 To add this step in the task sequence editor, click **Add**, select **Software**, and select **Install Package**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Install a single software package
 This setting specifies a Configuration Manager software package. The step waits until the installation completes.  

#### Install software packages according to dynamic variable list
 The task sequence installs packages using this base variable name. The base variable name is for a set of task sequence variables defined for a collection or computer. These variables specify the packages that the task sequence installs for that collection or computer. Each variable name consists of its common base name plus a numerical suffix starting at 001. The value for each variable must contain a package ID and the name of the software separated by a colon.  

 For the task sequence to install software by using a dynamic variable list, enable the following setting on the **Advanced** tab of the package **Properties**: **Allow this program to be installed from the Install Package task sequence without being deployed**.  

 > [!NOTE]  
 >  You can't install software packages by using a dynamic variable list for stand-alone media deployments.  

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

 - If you don't create the value of a variable in the correct format, or it doesn't specify a valid package ID and name, the software installation fails.  

 - If the package ID contains lowercase characters, the software installation fails.  

 - If the task sequence doesn't find a variable with the specified base name and "001" suffix, the task sequence doesn't install any packages. The task sequence continues.  

 > [!Important]  
 > These values are case-sensitive. For example, "install" is different than "Install". If you need to change the value, the task sequence editor doesn't detect a change of case. Make another edit at the same time, for example, modify the step description.<!--509714-->   

#### If installation of a software package fails, continue installing other packages in the list
 This setting specifies that the step continues if an individual software package installation fails. If you specify this setting, the task sequence continues regardless of any installation errors. If you don't specify this setting, and the installation fails, the step immediately ends.  



##  <a name="BKMK_InstallSoftwareUpdates"></a> Install Software Updates  

 Use this step to install software updates on the destination computer. The destination computer isn't evaluated for applicable software updates until this task sequence step runs. At that time, the destination computer is evaluated for software updates like any other Configuration Manager client. For this step to install software updates, first deploy the updates to a collection of which the target computer is a member.  

 > [!IMPORTANT]  
 > For best performance, install the latest version of the Windows Update Agent.  

 This task sequence step runs only in the full OS. It doesn't run in Windows PE. 

 Use the following task sequence variables with this step:
 - [SMSInstallUpdateTarget](/sccm/osd/understand/task-sequence-variables#SMSInstallUpdateTarget)
 - [SMSTSMPListRequestTimeoutEnabled](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeoutEnabled)
 - [SMSTSMPListRequestTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeout)
 - [SMSTSSoftwareUpdateScanTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout)
 - [SMSTSWaitForSecondReboot](/sccm/osd/understand/task-sequence-variables#SMSTSWaitForSecondReboot)

 > [!NOTE]  
 > If the client fails to retrieve the management point list from location services, use the **SMSTSMPListRequestTimeoutEnabled** and **SMSTSMPListRequestTimeout** variables. These variables specify how many milliseconds a task sequence waits before it retries installing an application or software update. For more information, see [Task sequence variables](task-sequence-variables.md).  

 To add this step in the task sequence editor, click **Add**, select **Software**, and select **Install Software Updates**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Required for installation - Mandatory software updates only
 Select this option to install all mandatory software updates with administrator-defined installation deadlines.  

#### Available for installation - All software updates
 Select this option to install all available software updates. First deploy these updates to a collection of which the computer is a member. The task sequence installs all available software updates on the destination computers.  

#### Evaluate software updates from cached scan results
 By default, this step uses cached scan results from the Windows Update Agent. Disable this option to instruct the Windows Update Agent to download the latest catalog from the software update point. Enable this option when using a task sequence to [capture and build an OS image](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system). A large number of software updates is likely in this scenario. 

 Many of these updates have dependencies. For example, install update ABC before update XYZ appears as applicable. When you disable this setting, and deploy the task sequence to many clients, they all connect to the software update point at the same time. This behavior results in performance issues during the process and download of the update catalog. 

 In most circumstances, use the default setting to use cached scan results. 

 The **SMSTSSoftwareUpdateScanTimeout** variable controls the software updates scan timeout during this step. The default value is 30 minutes. For more information, see [Task sequence variables](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout).


### Options   

 Besides the default options, configure the following additional settings on the **Options** tab of this task sequence step:  

#### Retry this step if computer unexpectedly restarts
 If one of the updates unexpectedly restarts the computer, retry this step. The step enables this setting by default with two retries. You can specify from one to five retries.  

 > [!NOTE]  
 > Configure the **SMSTSWaitForSecondReboot** variable to specify how many seconds the task sequence pauses after the computer restarts in this scenario. For more information, see [Task sequence variables](task-sequence-built-in-variables.md#SMSTSWaitForSecondReboot).  



##  <a name="BKMK_JoinDomainorWorkgroup"></a> Join Domain or Workgroup  

 Use this step to add the destination computer to a workgroup or domain.  

 This task sequence step runs only in the full OS. It doesn't run in Windows PE.   

 Use the following task sequence variables with this step:
 - [OSDJoinAccount](/sccm/osd/understand/task-sequence-variables#OSDJoinAccount)
 - [OSDJoinDomainName](/sccm/osd/understand/task-sequence-variables#OSDJoinDomainName)
 - [OSDJoinDomainOUName](/sccm/osd/understand/task-sequence-variables#OSDJoinDomainOUName)
 - [OSDJoinPassword](/sccm/osd/understand/task-sequence-variables#OSDJoinPassword)
 - [OSDJoinSkipReboot](/sccm/osd/understand/task-sequence-variables#OSDJoinSkipReboot)
 - [OSDJoinType](/sccm/osd/understand/task-sequence-variables#OSDJoinType)
 - [OSDJoinWorkgroupName](/sccm/osd/understand/task-sequence-variables#OSDJoinWorkgroupName)

 To add this step in the task sequence editor, click **Add**, select **General**, and select **Join Domain or Workgroup**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Join a workgroup
 Select this option to have the destination computer join the specified workgroup. If the computer is currently a member of a domain, selecting this option causes the computer to reboot.  

#### Join a domain
 Select this option to have the destination computer join the specified domain.  

 Optionally, enter or browse for an organizational unit (OU) in the specified domain for the computer to join. If the computer is currently a member of some other domain or a workgroup, this option causes the computer to reboot. If the computer is already a member of another OU, since Active Directory Domain Services doesn't allow changing the OU via this method, Windows Setup ignores this setting.  

#### Enter the account which has permission to join the domain
 Click **Set** to enter the username and password for an account with permissions to join the domain. Enter the account in the format:  `Domain\account`. For more information on the task sequence domain joining account, see [Accounts](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account).  



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Prepare ConfigMgr Client for Capture  

 Use this step to remove or configure the Configuration Manager client on the reference computer. This action prepares the computer for capture as part of the imaging process.

 This step completely removes the Configuration Manager client, instead of only removing key information. When the task sequence deploys the captured OS image, it installs a new Configuration Manager client each time.  

 > [!Note]  
 >  The task sequence engine only removes the client during the **Build and capture a reference operating system image** task sequence. The task sequence engine doesn't remove the client during other capture methods, such as capture media or a custom task sequence.  

 This task sequence step runs only in the full OS. It doesn't run in Windows PE.  

 To add this step in the task sequence editor, click **Add**, select **Images**, and select **Prepare ConfigMgr Client for Capture**. 


### Properties  

 This step doesn't require any settings on the **Properties** tab.



##  <a name="BKMK_PrepareWindowsforCapture"></a> Prepare Windows for Capture  

 Use this step to specify the Sysprep options when capturing an OS image on the reference computer. This step runs Sysprep, and then reboots the computer into the Windows PE boot image specified for the task sequence. This action fails if the reference computer is joined to a domain.  

 This step runs only in the full OS. It doesn't run in Windows PE.   

 Use the following task sequence variables with this step:
 - [OSDKeepActivation](/sccm/osd/understand/task-sequence-variables#OSDKeepActivation)
 - [OSDTargetSystemRoot](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemRoot-output)

 To add this step in the task sequence editor, click **Add**, select **Images**, and select **Prepare Windows for Capture**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Automatically build mass storage driver list
 Select this option to have Sysprep automatically build a list of mass storage drivers from the reference computer. This option enables the Build Mass Storage Drivers option in the sysprep.inf file on the reference computer. For more information about this setting, see the Sysprep documentation.  

#### Do not reset activation flag
 Select this option to prevent Sysprep from resetting the product activation flag.  

#### Shutdown the computer after running this action
 <!--SCCMDocs-pr issue 2695-->
 This option instructs Sysprep to shutdown the computer instead of its default restart behavior. 



##  <a name="BKMK_PreProvisionBitLocker"></a> Pre-provision BitLocker  

 Use this step to enable BitLocker on a drive while in Windows PE. Only the used drive space is encrypted, so encryption times are much faster. You apply the key management options by using the [Enable BitLocker](#BKMK_EnableBitLocker) step after the OS installs. 

 This step runs only in Windows PE. It doesn't run in the full OS.  

 > [!IMPORTANT]  
 >  Pre-provisioning BitLocker requires at least Windows 7. The computer must also contain a supported and enabled Trusted Platform Module (TPM).  

 To add this step in the task sequence editor, click **Add**, select **Disks**, and select **Pre-provision BitLocker**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Apply BitLocker to the specified drive
 Specify the drive for which you want to enable BitLocker. BitLocker only encrypts the used space on the drive.  

#### Skip this step for computers that do not have a TPM or when TPM is not enabled
 Select this option to skip drive encryption on a computer that doesn't contain a supported or enabled TPM. For example, use this option when you deploy an OS to a virtual machine.  



##  <a name="BKMK_ReleaseStateStore"></a> Release State Store  

 Use this step to notify the state migration point that the capture or restore action is complete. Use this step in conjunction with the **Request State Store**, **Capture User State**, and **Restore User State** steps. You use these steps to migrate user state data using a state migration point and the User State Migration Tool (USMT).  

 For more information about managing the user state when deploying operating systems, see [Manage user state](/sccm/osd/get-started/manage-user-state).  

 If you use the **Request State Store** step to request access to a state migration point to *capture* user state, this step notifies the state migration point that the capture process is complete. The state migration point then marks the user state data as available for restore. The state migration point sets the access control permissions for the user state data so that only the restoring computer has read-only access.  

 If you use the **Request State Store** step to request access to a state migration point to *restore* user state, this step notifies the state migration point that the restore process is complete. The state migration point then activates its configured data retention settings.  

 > [!IMPORTANT]  
 > Set the **Continue on Error** option for any steps between the **Request State Store** and **Release State Store** steps. Every **Request State Store** step must have a matching **Release State Store** step.  

 This step runs only in the full OS. It doesn't run in Windows PE.   

 Use the following task sequence variables with this step:
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)

 To add this step in the task sequence editor, click **Add**, select **User State**, and select **Release State Store**. 


### Properties  

 This step doesn't require any settings on the **Properties** tab.



##  <a name="BKMK_RequestStateStore"></a> Request State Store  

 Use this step to request access to a state migration point when capturing or restoring state.  

 For more information about managing the user state when deploying operating systems, see [Manage user state](/sccm/osd/get-started/manage-user-state).  

 Use this step in conjunction with the **Release State Store**, **Capture User State**, and **Restore User State** steps. You use these steps to migrate computer state using a state migration point and the User State Migration Tool (USMT).  

 > [!NOTE]  
 >  When creating a new state migration point, user state storage isn't available for up to one hour. To expedite availability, adjust any property settings on the state migration point to trigger a site control file update.  

 This step runs in the full OS and in Windows PE for offline USMT.   

 Use the following task sequence variables with this step:
 - [OSDStateFallbackToNAA](/sccm/osd/understand/task-sequence-variables#OSDStateFallbackToNAA)
 - [OSDStateSMPRetryCount](/sccm/osd/understand/task-sequence-variables#OSDStateSMPRetryCount)
 - [OSDStateSMPRetryTime](/sccm/osd/understand/task-sequence-variables#OSDStateSMPRetryTime)
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)

 To add this step in the task sequence editor, click **Add**, select **User State**, and select **Request State Store**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Capture state from the computer
 Find a state migration point that meets the minimum requirements as configured in the state migration point settings. For example, **Maximum number of clients** and **Minimum amount of free disk space**. This option doesn't guarantee sufficient space is available at the time of state migration. This option requests access to the state migration point for the purpose of capturing the user state and settings from a computer.  

 If the Configuration Manager site has multiple active state migration points, this step finds a state migration point with available disk space. The task sequence queries the management point for a list of state migration points, and then evaluates each until it finds one that meets the minimum requirements.  

#### Restore state from another computer
 Request access to a state migration point to restore previously captured user state and settings to a destination computer.  

 If there are multiple state migration points, this step finds the state migration point that has the state for the destination computer.  

#### Number of retries
 The number of times that this step tries to find an appropriate state migration point before failing.  

#### Retry delay (in seconds)
 The amount of time in seconds that the task sequence step waits between retry attempts.  

#### If computer account fails to connect to a state store, use the network access account
 If the task sequence can't access the state migration point using the computer account, it uses the network access account credentials to connect. This option is less secure because other computers could use the network access account to access the stored state. This option might be necessary if the destination computer isn't domain joined.  



##  <a name="BKMK_RestartComputer"></a> Restart Computer  

 Use this step to restart the computer running the task sequence. After the restart, the computer automatically continues with the next step in the task sequence.  

 This step can be run in either the full OS or Windows PE.   

 Use the following task sequence variables with this step:
 - [SMSRebootMessage](/sccm/osd/understand/task-sequence-variables#SMSRebootMessage)
 - [SMSRebootTimeout](/sccm/osd/understand/task-sequence-variables#SMSRebootTimeout)

 To add this step in the task sequence editor, click **Add**, select **General**, and select **Restart Computer**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### The boot image assigned to this task sequence
 Select this option for the destination computer to use the boot image assigned to the task sequence. The task sequence uses the boot image to run subsequent steps in Windows PE.  

#### The currently installed default operating system
 Select this option for the destination computer to reboot into the installed OS.  

#### Notify the user before restarting
 Select this option to display a notification to the user before the destination computer restarts. The step selects this option by default.  

#### Notification message
 Enter a notification message to display to the user before the destination computer restarts.  

#### Message display time-out
 Specify the amount of time in seconds before the destination computer restarts. The default is 60 seconds.  



##  <a name="BKMK_RestoreUserState"></a> Restore User State  

 Use this step to initiate the User State Migration Tool (USMT) to restore user state and settings to the destination computer. You use this step in conjunction with the **Capture User State** step.  

 For more information about managing the user state when deploying operating systems, see [Manage user state](/sccm/osd/get-started/manage-user-state).  

 Use this step with the **Request State Store** and **Release State Store** steps to save or restore the state settings with a state migration point. This option always decrypts the USMT state store by using an encryption key that Configuration Manager generates and manages.  

 The **Restore User State** step provides control over a limited subset of the most commonly used USMT options. Specify additional command-line options with the **OSDMigrateAdditionalRestoreOptions** variable.  

 > [!IMPORTANT]  
 >  If you're using this step for a purpose unrelated to an OS deployment scenario, add the [Restart Computer](#BKMK_RestartComputer) step immediately following the **Restore User State** step.  

 This step runs only in the full OS. It doesn't run in Windows PE.   

 Use the following task sequence variables with this step:
 - [_OSDMigrateUsmtRestorePackageID](/sccm/osd/understand/task-sequence-variables#OSDMigrateUsmtRestorePackageID)
 - [OSDMigrateAdditionalRestoreOptions](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdditionalRestoreOptions)
 - [OSDMigrateContinueOnRestore](/sccm/osd/understand/task-sequence-variables#OSDMigrateContinueOnRestore)
 - [OSDMigrateEnableVerboseLogging](/sccm/osd/understand/task-sequence-variables#OSDMigrateEnableVerboseLogging)
 - [OSDMigrateLocalAccounts](/sccm/osd/understand/task-sequence-variables#OSDMigrateLocalAccounts)
 - [OSDMigrateLocalAccountPassword](/sccm/osd/understand/task-sequence-variables#OSDMigrateLocalAccountPassword)
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)

 To add this step in the task sequence editor, click **Add**, select **User State**, and select **Restore User State**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### User state migration tool package
 Specify the package that contains the version of USMT for this step to use. This package doesn't require a program. When the step runs, the task sequence uses the version of USMT in the specified package. Specify a package containing the 32-bit or 64-bit version of USMT. The architecture of USMT depends upon the architecture of the OS to which the task sequence is restoring state. 

#### Restore all captured user profiles with standard options
 Restores the captured user profiles with the standard options. To customize the options that USMT restores, select **Customize user profile capture**.  

#### Customize how user profiles are restored
 Allows you to customize the files that you want to restore to the destination computer. Click **Files** to specify the configuration files in the USMT package you want to use for restoring the user profiles. To add a configuration file, enter the name of the file in the **Filename** box, and then click **Add**. The Files pane lists the configuration files that USMT uses. The .xml file you specify defines which user file USMT restores.  

#### Restore local computer user profiles
 Restores the local computer user profiles. These profiles aren't for domain users. Assign new passwords to the restored local user accounts. USMT can't migrate the original passwords. Enter the new password in the **Password** box, and confirm the password in the **Confirm Password** box.  

#### Continue if some files cannot be restored
 Continues restoring user state and settings even if USMT is unable to restore some files. The step enables this option by default. If you disable this option, and USMT encounters errors while restoring files, this step fails immediately. USMT doesn't restore all files.   

#### Enable verbose logging
 Enable this option to generate more detailed log file information. When restoring state, the task sequence by default generates **Loadstate.log** in the task sequence log folder, `%WinDir%\ccm\logs`.  



##  <a name="BKMK_RunCommandLine"></a> Run Command Line  

 Use this step to run the specified command line.  

 This step can be run in the full OS or Windows PE.   

 Use the following task sequence variables with this step:
 - [OSDDoNotLogCommand](/sccm/osd/understand/task-sequence-variables#OSDDoNotLogCommand) (starting in version 1806)<!--1358493-->
 - [SMSTSDisableWow64Redirection](/sccm/osd/understand/task-sequence-variables#SMSTSDisableWow64Redirection)
 - [SMSTSRunCommandLineUserName](/sccm/osd/understand/task-sequence-variables#SMSTSRunCommandLineUserName)
 - [SMSTSRunCommandLinePassword](/sccm/osd/understand/task-sequence-variables#SMSTSRunCommandLinePassword)
 - [WorkingDirectory](/sccm/osd/understand/task-sequence-variables#WorkingDirectory)

 To add this step in the task sequence editor, click **Add**, select **General**, and select **Run Command Line**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Command line
 Specifies the command line that the task sequence runs. This field is required. Include file name extensions, for example, .vbs and .exe. Include all required settings files and command-line options.  

 If you don't specify the file name extension, Configuration Manager tries .com, .exe, and .bat. If the file name has an extension that's not an executable type, Configuration Manager tries to apply a local association. For example, if the command line is readme.gif, Configuration Manager starts the application specified on the destination computer for opening .gif files.  

 Examples:  

 `setup.exe /a`  

 `cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

 > [!NOTE]  
 >  To run successfully, precede command-line actions with the **cmd.exe /c** command. Example of these actions include output redirection, piping, and copy commands.  

#### Disable 64-bit file system redirection
 By default, 64-bit operating systems use the WOW64 file system redirector to run command lines. This behavior is to properly find 32-bit versions of OS executables and libraries. Select this option to disable the use of the WOW64 file system redirector. Windows runs the command using native 64-bit versions of OS executables and libraries. This option has no effect when running on a 32-bit OS.  

#### Start in
 Specifies the executable folder for the program, up to 127 characters. This folder can be an absolute path on the destination computer or a path relative to the distribution point folder that contains the package. This field is optional.  

 Examples:  

 `c:\officexp`  

 `i386`  

 > [!NOTE]  
 >  The **Browse** button browses the local computer for files and folders. Anything you select must also exist on the destination computer. It must exist in the same location and with the same file and folder names.  

#### Package
 When you specify files or programs on the command line that aren't already present on the destination computer, select this option to specify the Configuration Manager package that contains the necessary files. The package doesn't require a program. If the specified files exist on the destination computer, this option isn't required.  

#### Time-out
 Specifies a value that represents how long Configuration Manager allows the command line to run. This value can be from one minute to 999 minutes. The default value is 15 minutes. This option is disabled by default.  

 > [!IMPORTANT]  
 >  If you enter a value that doesn't allow enough time for the specified command to complete successfully, this step fails. The entire task sequence could fail depending on step or group conditions. If the time-out expires, Configuration Manager terminates the command-line process.  

#### Run this step as the following account
 Specifies that the command line is run as a Windows user account other than the Local System account.  

 > [!NOTE]  
 >  To run simple scripts or commands with another account after installing the OS, first add the account to the computer. Additionally, you may need to restore Windows user profiles to run more complex programs, such as a Windows Installer.  

#### Account
 Specifies the Windows user account this step uses to run the command line. The command line runs with the permissions of the specified account. Click **Set** to specify the local user or domain account. For more information on the task sequence run-as account, see [Accounts](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account).

 > [!IMPORTANT]  
 >  If this step specifies a user account and runs in Windows PE, the action fails. You can't join Windows PE to a domain. The **smsts.log** file records this failure.  



##  <a name="BKMK_RunPowerShellScript"></a> Run PowerShell Script  

 Use this step to run the specified Windows PowerShell script.  

 This step can be run in the full OS or Windows PE. To run this step in Windows PE, enable PowerShell in the boot image. Enable the WinPE-PowerShell component from the **Optional Components** tab in the properties for the boot image. For more information about how to modify a boot image, see [Manage boot images](/sccm/osd/get-started/manage-boot-images).  

 > [!NOTE]  
 >  PowerShell isn't enabled by default on Windows Embedded operating systems.  

 To add this step in the task sequence editor, click **Add**, select **General**, and select **Run PowerShell Script**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Package
 Specify the Configuration Manager package that contains the PowerShell script. One package can contain multiple PowerShell scripts.  

#### Script name
 Specifies the name of the PowerShell script to run. This field is required.  

#### Parameters
 Specifies the parameters passed to the PowerShell script. These parameters are the same as the PowerShell script parameters on the command line.  

 > [!IMPORTANT]  
 >  Provide parameters consumed by the script, not for the Windows PowerShell command line.  
 >   
 >  The following example contains valid parameters:  
 >   
 >  `-MyParameter1 MyValue1 -MyParameter2 MyValue2`  
 >   
 >  The following example contains invalid parameters. The first two items are Windows PowerShell command-line parameters (**-NoLogo** and **-ExecutionPolicy Unrestricted**). The script doesn't consume these parameters.  
 >   
 >  `-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`  

#### PowerShell execution policy
 Determine which PowerShell scripts (if any) you allow to run on the computer. Choose one of the following execution policies:  

 -   **AllSigned**: Only run scripts signed by a trusted publisher  

 -   **Undefined**: Don't define any execution policy  

 -   **Bypass**: Load all configuration files and run all scripts. If you download an unsigned script from the internet, Windows PowerShell doesn't prompt for permission before running the script.  

 > [!IMPORTANT]  
 >  PowerShell 1.0 doesn't support Undefined and Bypass execution policies.  



##  <a name="child-task-sequence"></a> Run Task Sequence

 Beginning with Configuration Manager version 1710, you can add a new step that runs another task sequence. This step creates a parent-child relationship between the task sequences. With child task sequences, you can create more modular, reusable task sequences.

 Consider the following points when you add a child task sequence to a task sequence:  

 - The parent and child task sequences are effectively combined into a single policy that the client runs.  

 - The environment is global. If the parent task sequence sets a variable, and then the child task sequence changes that variable, it retains the latest value. If the child task sequence creates a new variable, it's available for the rest of the parent task sequence.  

 - Status messages are sent per normal for a single task sequence operation.  

 - The task sequence writes entries to the **smsts.log** file, with new log entries that make it clear when a child task sequence starts.  

 To add this step in the task sequence editor, click **Add**, select **General**, and select **Run Task Sequence**. 


### Properties

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Select task sequence to run
 Click **Browse** to select the child task sequence. The **Select a Task Sequence** dialog box doesn't display the parent task sequence.



##  <a name="BKMK_SetDynamicVariables"></a> Set Dynamic Variables  

 Use this step to perform the following actions:  

 1.  Gather information from the computer and its environment. Then set specified task sequence variables with the information.  

 2.  Evaluate defined rules. Set task sequence variables based on the rules that evaluate to true.  

 The task sequence automatically sets the following read-only task sequence variables:  
 - [\_SMSTSMake](/sccm/osd/understand/task-sequence-variables#SMSTSMake)  
 - [\_SMSTSModel](/sccm/osd/understand/task-sequence-variables#SMSTSModel)  
 - [\_SMSTSMacAddresses](/sccm/osd/understand/task-sequence-variables#SMSTSMacAddresses)  
 - [\_SMSTSIPAddresses](/sccm/osd/understand/task-sequence-variables#SMSTSIPAddresses)  
 - [\_SMSTSSerialNumber](/sccm/osd/understand/task-sequence-variables#SMSTSSerialNumber)  
 - [\_SMSTSAssetTag](/sccm/osd/understand/task-sequence-variables#SMSTSAssetTag)  
 - [\_SMSTSUUID](/sccm/osd/understand/task-sequence-variables#SMSTSUUID)  

 This step can be run in either the full OS or Windows PE.  

 To add this step in the task sequence editor, click **Add**, select **General**, and select **Set Dynamic Variables**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Dynamic rules and variables
 To set a dynamic variable for use in the task sequence, add a rule. Then set a value for each variable specified in the rule. Additionally, add one or more variables without adding a rule. When you add a rule, choose from the following categories:  

 - **Computer**: Evaluate values for hardware asset tag, UUID, serial number, or MAC address. Set multiple values as necessary. If any value is true, then the rule evaluates as true. For example, the following rule evaluates as true if the device serial number is 5892087 and the MAC address is 22-A4-5A-13-78-26:  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

 - **Location**: Evaluate values for the default network gateway  

 - **Make and Model**: Evaluate values for the make and model of a computer. Both the make and model must evaluate to true for the rule to evaluate to true.   

    Specify an asterisk (`*`) and question mark (`?`) as wild cards characters. The asterisk matches multiple characters and the question mark matches a single character. For example, the string `DELL*900?` matches both `DELL-ABC-9001` and `DELL9009`.  

 - **Task Sequence Variable**: Add a task sequence variable, condition, and value to evaluate. The rule evaluates to true when the value set for the variable meets the specified condition.  

    Specify one or more variables to set for a rule that evaluates to true, or set variables without using a rule. Select an existing variable, or create a custom variable.  

     - **Existing task sequence variables**: Select one or more variables from a list of existing task sequence variables. Array variables aren't available to select.  

     - **Custom task sequence variables**: Define a custom task sequence variable. You can also specify an existing task sequence variable. This setting is useful to specify an existing variable array, such as **OSDAdapter**, since variable arrays aren't in the list of existing task sequence variables.  

 After you select the variables for a rule, provide a value for each variable. The variable is set to the specified value when the rule evaluates to true. For each variable, you can select **Secret value** to hide the value of the variable. By default, some existing variables hide values, such as the **OSDCaptureAccountPassword** variable.  

 > [!IMPORTANT]  
 >  Configuration Manager removes any variable values marked as a **Secret value** when you import a task sequence with the **Set Dynamic Variables** step. Re-enter the value for the dynamic variable after you import the task sequence.  



##  <a name="BKMK_SetTaskSequenceVariable"></a> Set Task Sequence Variable  

 Use this step to set the value of a variable that's used with the task sequence.  

 This step can be run in either the full OS or Windows PE. 

 Task sequence variables are read by task sequence actions and specify the behavior of those actions. For more information about specific task sequence variables and how to use them, see the following articles:
- [How to use task sequence variables](/sccm/osd/understand/using-task-sequence-variables)
- [Task sequence variables](/sccm/osd/understand/task-sequence-variables)  

 To add this step in the task sequence editor, click **Add**, select **General**, and select **Set Task Sequence Variable**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Task sequence variable
 Specify the name of a task sequence built-in or action variable, or specify your own user-defined variable name.  

#### Do not display this value
<!--1358330-->
Starting in version 1806, enable this option to mask sensitive data stored in task sequence variables. For example, when specifying a password. 

#### Value  
 The task sequence sets the variable to this value. Set this task sequence variable to the value of another task sequence variable with the syntax `%varname%`.  



##  <a name="BKMK_SetupWindowsandConfigMgr"></a> Setup Windows and ConfigMgr  

 Use this step to perform the transition from Windows PE to the new OS. This task sequence step is a required part of any OS deployment. It installs the Configuration Manager client into the new OS, and prepares for the task sequence to continue execution in the new OS.  

 This step runs only in Windows PE. It doesn't run in the full OS.  

 Use the following task sequence variables with this step:
 - [SMSClientInstallProperties](/sccm/osd/understand/task-sequence-variables#SMSClientInstallProperties)

 This step replaces sysprep.inf or unattend.xml directory variables, such as `%WINDIR%` and `%ProgramFiles%`, with the Windows PE installation directory, `X:\Windows`. The task sequence ignores variables specified by using these environment variables.  

 To add this step in the task sequence editor, click **Add**, select **Images**, and select **Setup Windows and ConfigMgr**. 


### Step actions

 This step performs the following actions:  

#### Preliminaries: Windows PE  

 1.  Substitute task sequence variables in the unattend.xml file.  

 2.  Download the package that contains the Configuration Manager client. Add the package to the deployed image.  

#### Set up Windows  

 -  Image-based installation  

    1.  Disable the Configuration Manager client in the image, if it exists. In other words, disable Autostart for the Configuration Manager client service.  

    2.  Update the registry in the deployed image to start the deployed OS with the same drive letter as the reference computer.  

    3.  Restart to the deployed OS.  

    4.  Windows mini-setup runs by using the previously specified sysprep.inf or unattend.xml answer file that has all end-user interaction suppressed. If you use the **Apply Network Settings** step to join a domain, then that information is in the answer file. Windows mini-setup joins the computer to the domain.  

 -  Setup.exe-based installation. Runs Setup.exe that follows the typical Windows setup process:  

    1.  Copy the OS upgrade package, specified in the **Apply Operating System** step, to the hard disk drive.  

    2.  Restart to the newly deployed OS.  

    3.  Windows mini-setup runs by using the previously specified sysprep.inf or unattend.xml answer file that has all user interface settings suppressed. If you use the  **Apply Network Settings** step to join a domain, then that information is in the answer file. Windows mini-setup joins the computer to the domain.  

#### Set up the Configuration Manager client  

 1.  After Windows mini-setup finishes, the task sequence resumes by using setupcomplete.cmd.  

 2.  Enable or disable the local Administrator account, based on the option selected in the **Apply Windows Settings** step.  

 3.  Install the Configuration Manager client by using the previously downloaded package, and installation properties specified in this step. The client installs in "provisioning mode". This mode prevents the client from processing new policy requests until the task sequence completes.  

 4.  Wait for the client to be fully operational.  

#### The step completes
 The task sequence continues running the next step.  

<!-- Engineering confirmed that the task sequence does nothing with respect to group policy processing.
> [!NOTE]  
>  The **Setup Windows and ConfigMgr** task sequence action is responsible for running Group Policy on the newly installed computer. The Group Policy is applied after the task sequence is finished.  
-->


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Client package
 Click **Browse**, then select the Configuration Manager client installation package to use with this step.  

#### Use pre-production client package when available
 If there's a pre-production client package available, and the computer is a member of the piloting collection, the task sequence uses this package instead of the production client package. The pre-production client is a newer version for testing in the production environment. Click **Browse**, then select the pre-production client installation package to use with this step.  

#### Installation Properties
 The task sequence step automatically specifies site assignment and the default configuration. Use this field to specify any additional installation properties to use when you install the client. To enter multiple installation properties, separate them with a space.  

 Specify command-line options to use during client installation. For example, enter `/skipprereq: silverlight.exe` to inform CCMSetup.exe to not install the Microsoft Silverlight prerequisite. For more information about available command-line options for CCMSetup.exe, see [About client installation properties](/sccm/core/clients/deploy/about-client-installation-properties).  


### Options

 > [!NOTE]  
 > Don't enable **Continue on error** on the **Options** tab. If there's an error during this step, the task sequence fails whether or not you enable this setting.  



##  <a name="BKMK_UpgradeOS"></a> Upgrade Operating System  

 > [!TIP]  
 > Beginning with Windows 10, version 1709, media includes multiple editions. When you configure a task sequence to use an OS upgrade package or OS image, be sure to select a [supported edition](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).  

 Use this step to upgrade an older version of Windows to a newer version of Windows 10.  

 This task sequence step runs only in the full OS. It doesn't run in Windows PE.  

 Use the following task sequence variables with this step:
 - [_SMSTSOSUpgradeActionReturnCode](/sccm/osd/understand/task-sequence-variables#SMSTSOSUpgradeActionReturnCode)
 - [OSDSetupAdditionalUpgradeOptions](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions)

 To add this step in the task sequence editor, click **Add**, select **Images**, and select **Upgrade Operating System**. 


### Properties  

 On the **Properties** tab for this step, configure the settings described in this section.  

#### Upgrade package
 Select this option to specify the Windows 10 OS upgrade package to use for the upgrade.  

#### Source path
 Specifies a local or network path to the Windows 10 media that Windows Setup uses. This setting corresponds to the Windows Setup command-line option `/InstallFrom`. 

 You can also specify a variable, such as `%MyContentPath%` or `%DPC01%`. When you use a variable for the source path, set its value earlier in the task sequence. For example, use the [Download Package Content](#BKMK_DownloadPackageContent) step to specify a variable for the location of the OS upgrade package. Then, use that variable for the source path for this step.  

#### Edition
 Specify the edition within the OS media to use for the upgrade.  

#### Product key
 Specify the product key to apply to the upgrade process.  

#### Provide the following driver content to Windows Setup during upgrade
 Add drivers to the destination computer during the upgrade process. This setting corresponds to the Windows Setup command-line option `/InstallDriver`. The drivers must be compatible with Windows 10. Specify one of the following options:  

 - **Driver package**: Click **Browse** and select an existing driver package from the list.  

 - **Staged content**:  Select this option to specify the location for the driver package. You can specify a local folder, network path, or a task sequence variable. When you use a variable for the source path, set its value earlier in the task sequence. For example, by using the [Download Package Content](task-sequence-steps.md#BKMK_DownloadPackageContent) step.  

#### Time-out (minutes)
 Specify the number of minutes before Configuration Manager fails this step. This option is useful if Windows Setup stops processing but doesn't terminate.  

#### Perform Windows Setup compatibility scan without starting upgrade
 Perform the Windows Setup compatibility scan without starting the upgrade process. This setting corresponds to the Windows Setup command-line option `/Compat ScanOnly`. Deploy the entire OS upgrade package with this option. Setup returns an exit code as a result of the scan. The following table provides some of the more common exit codes:  

|Exit code|Details|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|No compatibility issues ("success").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Actionable compatibility issues.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|Selected migration choice isn't available. For example, an upgrade from Enterprise to Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Not eligible for Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Not enough free disk space.|  

For more information about this parameter, see [Windows Setup Command-Line Options](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#6).  

#### Ignore any dismissible compatibility messages
 Specifies that Setup completes the installation, ignoring any dismissible compatibility messages. This setting corresponds to the Windows Setup command-line option `/Compat IgnoreWarning`.  

#### Dynamically update Windows Setup with Windows Update
 Enable setup to perform Dynamic Update operations, such as search, download, and install updates. This setting corresponds to the Windows Setup command-line option `/DynamicUpdate`. This setting isn't compatible with Configuration Manager software updates. Enable this option when you manage updates with stand-alone Windows Server Update Services (WSUS) or Windows Update for Business.  

#### Override policy and use default Microsoft Update
 Temporarily override the local policy in real time to run Dynamic Update operations. The computer gets updates from Windows Update.
