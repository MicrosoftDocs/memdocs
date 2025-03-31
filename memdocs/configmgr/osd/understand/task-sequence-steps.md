---
title: Task sequence steps
titleSuffix: Configuration Manager
description: Learn about the steps that you can add to a Configuration Manager task sequence.
ms.date: 04/30/2024
ms.service: configuration-manager
ms.subservice: osd
ms.topic: reference
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz,frankroj
ms.collection: tier3
---

# Task sequence steps

*Applies to: Configuration Manager (current branch)*

The following task sequence steps can be added to a Configuration Manager task sequence. For more information, see [Use the task sequence editor](task-sequence-editor.md).

## Common settings

The following settings are common to all task sequence steps:

### Properties for all steps

- **Name**: The task sequence editor requires that you specify a short name to describe this step. When you add a new step, the task sequence editor sets the name to the Type by default. The **Name** length can't exceed 50 characters.

- **Description**: Optionally, specify more detailed information about this step. The **Description** length can't exceed 256 characters.

The rest of this article describes the other settings on the **Properties** tab for each task sequence step.

### Options for all steps

- **Disable this step**: The task sequence skips this step when it runs on a computer. The icon for this step is greyed out in the task sequence editor.

- **Continue on error**: If an error occurs while running the step, the task sequence continues. For more information, see [Planning considerations for automating tasks](../plan-design/planning-considerations-for-automating-tasks.md#task-sequence-groups).

- **Add Condition**: The task sequence evaluates these conditional statements to determine if it runs the step. For an example of using a task sequence variable as a condition, see [How to use task sequence variables](using-task-sequence-variables.md#bkmk_access-condition). For more information about conditions, see [Task sequence editor - Conditions](task-sequence-editor.md#bkmk_conditions).

The sections below for specific task sequence steps describe other possible settings on the **Options** tab.



## <a name="BKMK_ApplyDataImage"></a> Apply Data Image

Use this step to copy the data image to the specified destination partition.

This step runs only in Windows PE. It doesn't run in the full OS.

To add this step in the task sequence editor, select **Add**, select **Images**, and select **Apply Data Image**.

### Variables for Apply Data Image

Use the following task sequence variables with this step:

- [OSDDataImageIndex](task-sequence-variables.md#OSDDataImageIndex)
- [OSDWipeDestinationPartition](task-sequence-variables.md#OSDWipeDestinationPartition)

### Cmdlets for Apply Data Image

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Get-CMTSStepApplyDataImage)
- [New-CMTSStepApplyDataImage](/powershell/module/configurationmanager/New-CMTSStepApplyDataImage)
- [Remove-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Remove-CMTSStepApplyDataImage)
- [Set-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Set-CMTSStepApplyDataImage)

### Properties for Apply Data Image

On the **Properties** tab for this step, configure the settings described in this section.

#### Image Package

Select **Browse** to specify the **Image Package** used by this task sequence. Select the package you want to install in the **Select a Package** dialog box. The bottom of the dialog box displays the associated property information for each existing image package. Use the drop-down list to select the **Image** you want to install from the selected **Image Package**.

> [!NOTE]
> This task sequence action treats the image as a data file. This action doesn't do any setup to boot the image as an OS.

#### Destination

Configure one of the following options:

- **Next available partition**: Use the next sequential partition that an **Apply Operating System** or **Apply Data Image** step in this task sequence has not already targeted.

- **Specific disk and partition**: Select the **Disk** number (starting with 0) and the **Partition** number (starting with 1).

- **Specific logical drive letter**: Specify the **Drive Letter** that Windows PE assigns to the partition. This drive letter can be different from the drive letter assigned by the newly deployed OS.

- **Logical drive letter stored in a variable**: Specify the task sequence variable that contains the drive letter assigned to the partition by Windows PE. This variable is typically set in the Advanced section of the **Partition Properties** dialog box for the **Format and Partition Disk** task sequence step.

#### Delete all content on the partition before applying the image

Specifies that the task sequence deletes all files on the target partition before installing the image. By not deleting the content of the partition, this action can be used to apply additional content to a previously targeted partition.



## <a name="BKMK_ApplyDriverPackage"></a> Apply Driver Package

Use this step to download all of the drivers in the driver package and install them on the Windows OS.

The **Apply Driver Package** task sequence step makes all device drivers in a driver package available for use by Windows. Add this step between the **Apply Operating System** and **Setup Windows and ConfigMgr** steps to make the drivers in the package available to Windows. The **Apply Driver Package** task sequence step is also useful with stand-alone media deployment scenarios.

Put similar device drivers into a driver package, and distribute them to the appropriate distribution points. For example, put all drivers from one manufacturer into a driver package. Then distribute the package to distribution points where the associated computers can access them.

The **Apply Driver Package** step is useful for stand-alone media. This step is also useful to install a specific set of drivers. These types of drivers include devices that Windows plug-and-play doesn't detect, such as network printers.

This task sequence step runs only in Windows PE. It doesn't run in the full OS.

To add this step in the task sequence editor, select **Add**, select **Drivers**, and select **Apply Driver Package**.

> [!TIP]
> For an overview on drivers in Configuration Manager, see [Use task sequences to install drivers](../get-started/manage-drivers.md#BKMK_TSDrivers).
>
> Use content pre-caching to download an applicable driver package before a user installs the task sequence. For more information, see [Configure pre-cache content](../deploy-use/configure-precache-content.md).

### Variables for Apply Driver Package

Use the following task sequence variables with this step:

- [OSDApplyDriverBootCriticalContentUniqueID](task-sequence-variables.md#OSDApplyDriverBootCriticalContentUniqueID)
- [OSDApplyDriverBootCriticalHardwareComponent](task-sequence-variables.md#OSDApplyDriverBootCriticalHardwareComponent)
- [OSDApplyDriverBootCriticalID](task-sequence-variables.md#OSDApplyDriverBootCriticalID)
- [OSDApplyDriverBootCriticalINFFile](task-sequence-variables.md#OSDApplyDriverBootCriticalINFFile)
- [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions)<!--516679/2840016-->

### Cmdlets for Apply Driver Package

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Get-CMTSStepApplyDriverPackage)
- [New-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/New-CMTSStepApplyDriverPackage)
- [Remove-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Remove-CMTSStepApplyDriverPackage)
- [Set-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Set-CMTSStepApplyDriverPackage)

### Properties for Apply Driver Package

On the **Properties** tab for this step, configure the settings described in this section.

#### Driver package

Specify the driver package that contains the needed device drivers. Select **Browse** to launch the **Select a Package** dialog box. Select an existing driver package to apply. The bottom of the dialog box displays the associated package properties.

#### Install driver package via running DISM with recurse option

Select this option to add the `/recurse` parameter to the DISM command line when Windows applies the driver package.

When you enable this option, you can also specify additional DISM command-line parameters. Use the [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions) task sequence variable to include more options. For more information, see [Windows DISM Command-Line Options](/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).<!-- SCCMDocs#2125 -->

#### Select the mass storage driver within the package that needs to be installed before setup on pre-Windows Vista operating systems

Specify any mass storage drivers needed to install a classic OS.

##### Driver

Select the mass storage driver file to install before setup of a classic OS. The drop-down list populates from the specified package.

##### Model

Specify the boot-critical device that is needed for pre-Windows Vista OS deployments.

#### Do unattended installation of unsigned drivers on version of Windows where this is allowed

This option allows Windows to install drivers without a digital signature.



## <a name="BKMK_ApplyNetworkSettings"></a> Apply Network Settings

Use this step to specify the network or workgroup configuration information for the destination computer. The task sequence stores these values in the appropriate answer file. Windows Setup uses this answer file during the **Setup Windows and ConfigMgr** action.

This task sequence step runs only in Windows PE. It doesn't run in the full OS.

To add this step in the task sequence editor, select **Add**, select **Settings**, and select **Apply Network Settings**.

> [!NOTE]
> If you include multiple instances of this step in a task sequence, conditions don't apply. The settings from the last instance of this step in the task sequence are applied to the device. To work around this behavior, include each step in a separate group with conditions on the group.

### Variables for Apply Network Settings

Use the following task sequence variables with this step:

- [OSDAdapter](task-sequence-variables.md#OSDAdapter)
- [OSDAdapterCount](task-sequence-variables.md#OSDAdapterCount)
- [OSDDNSDomain](task-sequence-variables.md#OSDDNSDomain)
- [OSDDNSSuffixSearchOrder](task-sequence-variables.md#OSDDNSSuffixSearchOrder)
- [OSDDomainName](task-sequence-variables.md#OSDDomainName)
- [OSDDomainOUName](task-sequence-variables.md#OSDDomainOUName)
- [OSDEnableTCPIPFiltering](task-sequence-variables.md#OSDEnableTCPIPFiltering)
- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)
- [OSDWorkgroupName](task-sequence-variables.md#OSDWorkgroupName)

### Cmdlets for Apply Network Settings

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyNetworkSetting)
- [New-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/New-CMTSStepApplyNetworkSetting)
- [Remove-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Remove-CMTSStepApplyNetworkSetting)
- [Set-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Set-CMTSStepApplyNetworkSetting)
- [New-CMTSNetworkAdapterSetting](/powershell/module/configurationmanager/new-cmtsnetworkadaptersetting)

### Properties for Apply Network Settings

On the **Properties** tab for this step, configure the settings described in this section.

#### Join a workgroup

Select this option to have the destination computer join the specified workgroup. Enter the name of the workgroup on the **Workgroup** line. The value that the **Capture Network Settings** task sequence step captures can override this value.

#### Join a domain

Select this option to have the destination computer join the specified domain. Specify or browse to the domain, such as `fabricam.com`. Specify or browse to a Lightweight Directory Access Protocol (LDAP) path for an organizational unit. For example: `LDAP//OU=computers, DC=Fabricam.com, C=com`.

> [!NOTE]
> When a Microsoft Entra joined client runs an OS deployment task sequence, the client in the new OS won't automatically join Microsoft Entra ID. Even though it's not Microsoft Entra joined, the client is still managed.

#### Account

Select **Set** to specify an account with the necessary permissions to join the computer to the domain. In the **Windows User Account** dialog box, enter the user name in the following format: `Domain\User`. For more information, see [Domain joining account](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).

#### Adapter settings

Specify network configurations for each network adapter in the computer. Select **New** to open the **Network Settings** dialog box, and then specify the network settings.

- If you also use the **Capture Network Settings** step, the task sequence applies the previously captured settings to the network adapter.
- If the task sequence didn't previously capture network settings, it applies the settings you specify in this step.
- The task sequence applies these settings to network adapters in Windows device enumeration order.
- The task sequence doesn't immediately apply the settings you specify in this step to the computer.



## <a name="BKMK_ApplyOperatingSystemImage"></a> Apply Operating System Image

Use this step to install an OS on the destination computer.

After the **Apply Operating System** action runs, it sets the **OSDTargetSystemDrive** variable to the drive letter of the partition containing the OS files.

This task sequence step runs only in Windows PE. It doesn't run in the full OS.

To add this step in the task sequence editor, select **Add**, select **Images**, and select **Apply Operating System Image**.

> [!TIP]
> Windows 11 and Windows 10 media include multiple editions. When you configure a task sequence to use an OS upgrade package or OS image, be sure to select a [supported edition](../../core/plan-design/configs/support-for-windows-11.md#support-notes).
>
> Use content pre-caching to download an applicable OS upgrade package before a user installs the task sequence. For more information, see [Configure pre-cache content](../deploy-use/configure-precache-content.md).
>
> The **Setup Windows and ConfigMgr** step starts the installation of Windows.

### Variables for Apply OS Image

Use the following task sequence variables with this step:

- [OSDConfigFileName](task-sequence-variables.md#OSDConfigFileName)
- [OSDImageIndex](task-sequence-variables.md#OSDImageIndex)
- [OsdLayeredDriver](task-sequence-variables.md#OsdLayeredDriver)
- [OSDTargetSystemDrive](task-sequence-variables.md#OSDTargetSystemDrive)

### Cmdlets for Apply OS Image

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepApplyOperatingSystem)
- [New-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/New-CMTSStepApplyOperatingSystem)
- [Remove-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Remove-CMTSStepApplyOperatingSystem)
- [Set-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Set-CMTSStepApplyOperatingSystem)

### Behaviors for Apply OS Image

This step performs different actions depending on whether it uses an OS image or an OS upgrade package.

#### OS image actions

The **Apply Operating System Image** step performs the following actions when using an OS image:

1. Delete all content on the targeted volume, except files in the folder specified by the **\_SMSTSUserStatePath** variable.

2. Extract the contents of the specified .wim file to the specified destination partition.

3. Prepare the answer file:

    1. Create a new default Windows Setup answer file (sysprep.inf or unattend.xml) for the deployed OS.

    2. Merge any values from the user-supplied answer file.

4. Copy Windows boot loaders into the active partition.

5. Set the boot.ini or the Boot Configuration Database (BCD) to reference the newly installed OS.

#### OS upgrade package actions

The **Apply Operating System Image** step performs the following actions when using an OS upgrade package:

1. Delete all content on the targeted volume, except files in the folder specified by the **\_SMSTSUserStatePath** variable.

2. Prepare the answer file:

    1. Create a fresh answer file with standard values created by Configuration Manager.

    2. Merge any values from the user-supplied answer file.

### Properties for Apply OS Image

On the **Properties** tab for this step, configure the settings described in this section.

#### Apply operating system from a captured image

Installs an OS image that you captured. Select **Browse** to open the **Select a package** dialog box. Then select the existing image package you want to install. If multiple images are associated with the specified **Image package**, select from the drop-down list the associated image to use for this deployment. You can view basic information about each existing image by selecting it.

#### Apply operating system image from an original installation source

Installs an OS using an OS upgrade package, which is also an original installation source. Select **Browse** to open the **Select an Operating System Upgrade Package** dialog box. Then select the existing OS upgrade package you want to use. You can view basic information about each existing image source by selecting it. The results pane at the bottom of the dialog box displays the associated image source properties. If there are multiple editions associated with the specified package, use the drop-down list to select the **Edition** you want to use.

> [!NOTE]
> **Operating System Upgrade Packages** are primarily meant for use with in-place upgrades and not for new installations of Windows. When deploying new installations of Windows, use the **Apply operating system from a captured image** option and **install.wim** from the installation source files.
>
> Deploying new installations of Windows via **Operating System Upgrade Packages** is still supported, but it's dependent on drivers being compatible with this method. When installing Windows from an OS upgrade package, drivers are installed while still in Windows PE versus simply being injected while in Windows PE. Some drivers aren't compatible with being installed while in Windows PE.
>
> If drivers aren't compatible with being installed while in Windows PE, then create an **Operating System Image** with the **install.wim** from the original installation source files. Then deploy via the **Apply operating system from a captured image** option instead.

#### Use an unattended or sysprep answer file for a custom installation

Use this option to provide a Windows setup answer file (**unattend.xml**, **unattend.txt**, or **sysprep.inf**) depending on the OS version and installation method. The file you specify can include any of the standard configuration options supported by Windows answer files. For example, you can use it to specify the default Internet Explorer home page. Specify the package that contains the answer file and the associated path to the file in the package.

> [!NOTE]
> The Windows setup answer file that you supply can contain embedded task sequence variables of the form `%varname%`, where *varname* is the name of the variable. The **Setup Windows and ConfigMgr** step substitutes the variable string for the actual value of the variable. You can't use these embedded task sequence variables in numeric-only fields in an unattend.xml answer file.

If you don't supply a Windows setup answer file, the task sequence automatically generates an answer file.

#### Destination

Configure one of the following options:

- **Next available partition**: Use the next sequential partition not already targeted by an **Apply Operating System** or **Apply Data Image** step in this task sequence.

- **Specific disk and partition**: Select the **Disk** number (starting with 0) and the **Partition** number (starting with 1).

- **Specific logical drive letter**: Specify the **Drive Letter** assigned to the partition by Windows PE. This drive letter can be different from the drive letter assigned by the newly deployed OS.

- **Logical drive letter stored in a variable**: Specify the task sequence variable containing the drive letter assigned to the partition by Windows PE. This variable is typically set in the Advanced section of the **Partition Properties** dialog box for the **Format and Partition Disk** task sequence step.

#### Select layered driver if applicable

<!--9735002-->
Version 2107 and later supports layered keyboard drivers. These drivers specify other types of keyboards that are common with Japanese and Korean languages. For more information, see the [LayeredDriver](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-winpe-layereddriver) Windows setting.

Choose one of the following options:

- **Do not specify**: This option is the default, which doesn't configure the LayeredDriver setting in the unattend.xml. This behavior is consistent with earlier versions of Configuration Manager.
- **PC/AT Enhanced keyboard (101/102-key)**
- **Korean PC/AT 101-Key Compatible keyboard or the Microsoft Natural keyboard (type 1)**
- **Korean PC/AT 101-Key Compatible keyboard or the Microsoft Natural keyboard (type 2)**
- **Korean PC/AT 101-Key Compatible keyboard or the Microsoft Natural keyboard (type 3)**
- **Korean keyboard (103/106-key)**
- **Japanese keyboard (106/109-key)**

You can also use the [OsdLayeredDriver](task-sequence-variables.md#OsdLayeredDriver) task sequence variable.

### Options for Apply OS Image

Besides the default options, configure the following additional settings on the **Options** tab of this task sequence step:

#### Access content directly from the distribution point

Configure the task sequence to access the OS image directly from the distribution point. For example, use this option when you deploy operating systems to embedded devices that have limited storage capacity. When selecting this option, also configure the package share settings on the **Data Access** tab of the OS image properties.

> [!NOTE]
> This setting overrides the deployment option that you configure on the **Distribution Points** page in the **Deploy Software Wizard**. This override is only for the OS image that this step specifies, not for all task sequence content.

> [!IMPORTANT]
> For greatest security, it is strongly recommended not to select this option. This option is mainly designed for use on devices with limited storage capacity. This option is not meant to help increase the speed of the task sequence. When this option is selected, the package hash is not verified for the operating system package. Therefore, package integrity cannot be ensured because it is possible for users with administrative rights to alter or tamper with package contents.



## <a name="BKMK_ApplyWindowsSettings"></a> Apply Windows Settings

Use this step to configure the Windows settings for the destination computer. The task sequence stores these values in the appropriate answer file. Windows Setup uses this answer file during the **Setup Windows and ConfigMgr** step.

This task sequence step runs only in Windows PE. It doesn't run in the full OS.

To add this step in the task sequence editor, select **Add**, select **Settings**, and select **Apply Windows Settings**.

### Variables for Apply Windows Settings

Use the following task sequence variables with this step:

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-input)
- [OSDLocalAdminPassword](task-sequence-variables.md#OSDLocalAdminPassword)
- [OSDProductKey](task-sequence-variables.md#OSDProductKey)
- [OSDRandomAdminPassword](task-sequence-variables.md#OSDRandomAdminPassword)
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-input)
- [OSDRegisteredUserName](task-sequence-variables.md#OSDRegisteredUserName)
- [OSDServerLicenseConnectionLimit](task-sequence-variables.md#OSDServerLicenseConnectionLimit)
- [OSDServerLicenseMode](task-sequence-variables.md#OSDServerLicenseMode)
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-input)
- [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale)
- [OSDWindowsSettingsSystemLocale](task-sequence-variables.md#OSDWindowsSettingsSystemLocale)
- [OSDWindowsSettingsUILanguage](task-sequence-variables.md#OSDWindowsSettingsUILanguage)
- [OSDWindowsSettingsUILanguageFallback](task-sequence-variables.md#OSDWindowsSettingsUILanguageFallback)
- [OSDWindowsSettingsUserLocale](task-sequence-variables.md#OSDWindowsSettingsUserLocale)

### Cmdlets for Apply Windows Settings

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting)
- [New-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting)
- [Remove-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Remove-CMTSStepApplyWindowsSetting)
- [Set-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Set-CMTSStepApplyWindowsSetting)

### Properties for Apply Windows Settings

On the **Properties** tab for this step, configure the settings described in this section.

#### User name

Specify the registered user name to associate with the destination computer. The value that the **Capture Windows Settings** task sequence step captures can override this value.

#### Organization name

Specify the registered organization name to associate with the destination computer. The value that the **Capture Windows Settings** task sequence step captures can override this value.

#### Product key

Specify the product key to use for the Windows installation on the destination computer.

#### Server licensing

> [!NOTE]
> This setting only applies to legacy versions of Windows that are no longer supported.<!-- #4833 --> Starting in version 2010, the setting is no longer visible in the task sequence editor. Existing task sequences that still use this setting will continue to function the same.<!-- 7035424 -->

#### Maximum connections

> [!NOTE]
> This setting only applies to legacy versions of Windows that are no longer supported.<!-- #4833 --> Starting in version 2010, the setting is no longer visible in the task sequence editor. Existing task sequences that still use this setting will continue to function the same.<!-- 7035424 -->

#### Randomly generate the local administrator password and disable the account on all supported platforms (recommended)

Select this option to set the local administrator password to a randomly generated string. This option also disables the local administrator account on platforms that support this capability.

#### Enable the account and specify the local administrator password

Select this option to enable the local administrator account using the specified password. Enter the password on the **Password** line and confirm the password on the **Confirm password** line.

#### Time zone

Specify the time zone to configure on the destination computer. The value that the **Capture Windows Settings** task sequence step captures can override this value.

#### Language settings

<!--5411057, 5138936-->

Use these settings to control the language configuration during OS deployment. If you're already applying these language settings, this change can help you simplify your OS deployment task sequence. Instead of using multiple steps per language or separate scripts, use one instance per language of this step with a condition for that language.

Configure the following settings:

- Input locale (default keyboard layout)
- System locale
- UI language
- UI language fallback
- User locale

For more information on these Windows setup answer file values, see [Microsoft-Windows-International-Core](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core).

> [!NOTE]
> If you create a custom Windows setup answer file (unattend.xml), this step overwrites any existing values. To automate a dynamic process for these settings, use the related task sequence variables. For example, [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale).

## <a name="BKMK_AutoApplyDrivers"></a> Auto Apply Drivers

Use this step to match and install drivers as part of the OS deployment.

> [!IMPORTANT]
> Stand-alone media can't use the **Auto Apply Drivers** step. The task sequence has no connection to the Configuration Manager site in this scenario.

This task sequence step runs only in Windows PE. It doesn't run in the full OS.

To add this step in the task sequence editor, select **Add**, select **Drivers**, and select **Auto Apply Drivers**.

> [!TIP]
> For an overview of drivers in Configuration Manager, see [Use task sequences to install drivers](../get-started/manage-drivers.md#BKMK_TSDrivers).

### Behaviors for Auto Apply Drivers

The **Auto Apply Drivers** task sequence step performs the following actions:

1. Scan the hardware and find the plug-and-play IDs for all devices present on the system.

2. Send the list of devices and their plug-and-play IDs to the management point. The management point returns a list of compatible drivers from the driver catalog for each hardware device. The list includes all enabled drivers regardless of what driver package they are in, and drivers tagged with the specified driver category.

3. For each hardware device, the task sequence picks the best driver. This driver is appropriate for the deployed OS, and is on an accessible distribution point.

4. The task sequence downloads the selected drivers from a distribution point, and stages the drivers on the target OS.

    1. When using an OS image, the task sequence places the drivers into the OS driver store.

    2. When using an OS upgrade package as an original installation source, the task sequence configures Windows Setup with the drivers' location.

5. During the **Setup Windows and ConfigMgr** step in the task sequence, Windows Setup finds the drivers staged by this step.

### Variables for Auto Apply Drivers

Use the following task sequence variables with this step:

- [OSDAutoApplyDriverBestMatch](task-sequence-variables.md#OSDAutoApplyDriverBestMatch)
- [OSDAutoApplyDriverCategoryList](task-sequence-variables.md#OSDAutoApplyDriverCategoryList)
- [SMSTSDriverRequestConnectTimeOut](task-sequence-variables.md#SMSTSDriverRequestConnectTimeOut)
- [SMSTSDriverRequestReceiveTimeOut](task-sequence-variables.md#SMSTSDriverRequestReceiveTimeOut)
- [SMSTSDriverRequestResolveTimeOut](task-sequence-variables.md#SMSTSDriverRequestResolveTimeOut)
- [SMSTSDriverRequestSendTimeOut](task-sequence-variables.md#SMSTSDriverRequestSendTimeOut)

### Cmdlets for Auto Apply Drivers

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Get-CMTSStepAutoApplyDriver)
- [New-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/New-CMTSStepAutoApplyDriver)
- [Remove-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Remove-CMTSStepAutoApplyDriver)
- [Set-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Set-CMTSStepAutoApplyDriver)

### Properties for Auto Apply Drivers

On the **Properties** tab for this step, configure the settings described in this section.

#### Install only the best matched compatible drivers

Specifies that the task sequence step installs only the best matched driver for each hardware device detected.

#### Install all compatible drivers

The task sequence installs all drivers compatible for each detected hardware device. Windows Setup then chooses the best driver. This option takes more network bandwidth and disk space. The task sequence downloads more drivers, but Windows can select a better driver.

#### Consider drivers from all categories

The task sequence searches all available driver categories for the appropriate device drivers.

#### Limit driver matching to only consider drivers in selected categories

The task sequence searches in the specified driver categories for the appropriate device drivers.

If you select multiple categories, it returns all matching drivers that are present in any of the categories. It's equivalent to an `OR` operation.<!-- SCCMDocs issue 851 -->

#### Do unattended installation of unsigned drivers on versions of Windows where this is allowed

This option allows Windows to install drivers without a digital signature.

> [!IMPORTANT]
> This option doesn't apply to operating systems where you can't configure driver signing policy.



## <a name="BKMK_CaptureNetworkSettings"></a> Capture Network Settings

Use this step to capture Microsoft network settings from the computer running the task sequence. The task sequence saves these settings in task sequence variables. These settings override the default settings you configure on the **Apply Network Settings** step.

This task sequence step runs only in the full OS. It doesn't run in Windows PE.

To add this step in the task sequence editor, select **Add**, select **Settings**, and select **Capture Network Settings**.

### Variables for Capture Network Settings

Use the following task sequence variables with this step:

- [OSDMigrateAdapterSettings](task-sequence-variables.md#OSDMigrateAdapterSettings)
- [OSDMigrateNetworkMembership](task-sequence-variables.md#OSDMigrateNetworkMembership)

### Cmdlets for Capture Network Settings

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Get-CMTSStepCaptureNetworkSettings)
- [New-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/New-CMTSStepCaptureNetworkSettings)
- [Remove-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Remove-CMTSStepCaptureNetworkSettings)
- [Set-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Set-CMTSStepCaptureNetworkSettings)

### Properties for Capture Network Settings

On the **Properties** tab for this step, configure the settings described in this section.

#### Migrate domain and workgroup membership

Captures the domain and workgroup membership information of the destination computer.

#### Migrate network adapter configuration

Captures the network adapter configuration of the destination computer. It captures the following information:

- Global network settings
- Number of adapters
- The following network settings associated with each adapter: DNS, IP, and port filters



## <a name="BKMK_CaptureOperatingSystemImage"></a> Capture Operating System Image

This step captures one or more images from a reference computer. The task sequence creates a Windows image (.wim) file on the specified network share. Then use the **Add Operating System Image Package** wizard to import this image into Configuration Manager for image-based OS deployments.

Configuration Manager captures each volume (drive) from the reference computer to a separate image within the .wim file. If the referenced computer has multiple volumes, the resulting .wim file contains a separate image for each volume. This step only captures volumes that are formatted as NTFS or FAT32. It skips volumes with other formats, and USB volumes.

The installed OS on the reference computer must be a version of Windows that Configuration Manager supports. Use the SysPrep tool to prepare the OS on the reference computer. The installed OS volume and the boot volume must be the same volume.

Specify an account with write permissions to the selected network share. For more information on the capture OS image account, see [Accounts](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

This task sequence step runs only in Windows PE. It doesn't run in the full OS.

To add this step in the task sequence editor, select **Add**, select **Images**, and select **Capture Operating System Image**.

### Variables for Capture OS Image

Use the following task sequence variables with this step:

- [OSDCaptureAccount](task-sequence-variables.md#OSDCaptureAccount)
- [OSDCaptureAccountPassword](task-sequence-variables.md#OSDCaptureAccountPassword)
- [OSDCaptureDestination](task-sequence-variables.md#OSDCaptureDestination)
- [OSDImageCreator](task-sequence-variables.md#OSDImageCreator)
- [OSDImageDescription](task-sequence-variables.md#OSDImageDescription)
- [OSDImageVersion](task-sequence-variables.md#OSDImageVersion)
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-input)

### Cmdlets for Capture OS Image

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Get-CMTSStepCaptureSystemImage)
- [New-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/New-CMTSStepCaptureSystemImage)
- [Remove-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Remove-CMTSStepCaptureSystemImage)
- [Set-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Set-CMTSStepCaptureSystemImage)

### Properties for Capture OS Image

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

Enter the Windows account that has permissions to the specified network share. Select **Set** to specify the name of the Windows account.



## <a name="BKMK_CaptureUserState"></a> Capture User State

This step uses the User State Migration Tool (USMT) to capture user state and settings from the computer running the task sequence. This task sequence step is used in conjunction with the **Restore User State** task sequence step. This step always encrypts the USMT state store by using an encryption key that Configuration Manager generates and manages.

Starting in version 2103, this step and the **Restore User State** step use the current highest supported encryption algorithm, **AES 256**.<!--9171505-->

> [!IMPORTANT]
> If you have any active user state migrations, before you update the Configuration Manager client on those devices, restore the user state. Otherwise, the updated client will fail to restore the user state when it tries to use a different encryption algorithm. If necessary, you can manually restore the user state and explicitly use the USMT parameter `/decrypt:3DES`.

For more information about managing the user state when deploying operating systems, see [Manage user state](../get-started/manage-user-state.md).

If you want to save and restore user state settings from a state migration point, use this step with the **Request State Store** and **Release State Store** steps.

This step provides control over a limited subset of the most commonly used USMT options. Specify additional command-line options using the **OSDMigrateAdditionalCaptureOptions** task sequence variable.

This task sequence step runs in either Windows PE or the full OS.

To add this step in the task sequence editor, select **Add**, select **User State**, and select **Capture User State**.

### Variables for Capture User State

Use the following task sequence variables with this step:

- [_OSDMigrateUsmtPackageID](task-sequence-variables.md#OSDMigrateUsmtPackageID)
- [OSDMigrateAdditionalCaptureOptions](task-sequence-variables.md#OSDMigrateAdditionalCaptureOptions)
- [OSDMigrateConfigFiles](task-sequence-variables.md#OSDMigrateConfigFiles)
- [OSDMigrateContinueOnLockedFiles](task-sequence-variables.md#OSDMigrateContinueOnLockedFiles)
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)
- [OSDMigrateMode](task-sequence-variables.md#OSDMigrateMode)
- [OSDMigrateSkipEncryptedFiles](task-sequence-variables.md#OSDMigrateSkipEncryptedFiles)
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)

### Cmdlets for Capture User State

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Get-CMTSStepCaptureUserState)
- [New-CMTSStepCaptureUserState](/powershell/module/configurationmanager/New-CMTSStepCaptureUserState)
- [Remove-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Remove-CMTSStepCaptureUserState)
- [Set-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Set-CMTSStepCaptureUserState)

### Properties for Capture User State

On the **Properties** tab for this step, configure the settings described in this section.

#### User state migration tool package

Specify the package that contains the User State Migration Tool (USMT). The task sequence uses this version of USMT to capture the user state and settings. This package doesn't require a program. Specify a package containing the 32-bit or 64-bit version of USMT. The architecture of USMT depends upon the architecture of the OS from which the task sequence is capturing state.

#### Capture all user profiles by using standard options

Migrate all user profile information. This option is the default.

If you select this option, but don't select **Restore local computer user profiles** in the **Restore User State** step, the task sequence fails. Configuration Manager can't migrate the new accounts without assigning them passwords.

When you use the **Install an existing image package** option of the **New Task Sequence** wizard, the resulting task sequence defaults to **Capture all user profiles with standard options**. This default task sequence doesn't select the option to **Restore local computer user profiles**, or non-domain user accounts.

Select **Restore local computer user profiles** and provide a password for the account to migrate. In a manually created task sequence, this setting is found under the **Restore User State** step. In a task sequence created by the **New Task Sequence** wizard, this setting is found under the step **Restore User Files and Settings** wizard page.

If you have no local user accounts, this setting doesn't apply.

#### Customize how user profiles are captured

Select this option to specify a custom profile file for migration. Select **Files** to select the configuration files for USMT to use with this step. Specify a custom .xml file that contains rules that define the user state files to migrate.

#### Select configuration files

Choose this option and select **Files** to select the configuration files in the USMT package you want to use to capture user profiles. To add a configuration file, enter the **Filename** and select **Add**.

#### Enable verbose logging

Enable this option to generate more detailed log file information. When capturing state, the task sequence by default generates **ScanState.log** in the task sequence log folder, `%WinDir%\ccm\logs`.

#### Skip files using encrypted file system

Enable this option to skip capturing files encrypted with the Encrypted File System (EFS). These files include user profile files. Depending on the OS and USMT versions, encrypted files might not be readable after you restore. For more information, see the USMT documentation.

#### Copy by using file system access

Enable this option to specify any of the following settings:

- **Continue if some files cannot be captured**: Enable this setting to continue the migration process even if it can't capture some files. If you disable this option, and a file can't be captured, then this step fails. This option is enabled by default.

- **Capture locally by using links instead of by copying files**: Enable this setting to use NTFS hard-links to capture files.

    For more information about migrating data using hard-links, see [Hard-Link Migration Store](/windows/deployment/usmt/usmt-hard-link-migration-store).

- **Capture in off-line mode (Windows PE only)**: Enable this setting to capture the user state while in Windows PE instead of the full OS.

#### Capture by using Volume Copy Shadow Services (VSS)

This option allows you to capture files even if they're locked for editing by another application.



## <a name="BKMK_CaptureWindowsSettings"></a> Capture Windows Settings

Use this step to capture the Windows settings from the computer running the task sequence. The task sequence saves these settings in task sequence variables. These captured settings override the default settings that you configure on the **Apply Windows Settings** step.

This task sequence step runs in either Windows PE or the full OS.

To add this step in the task sequence editor, select **Add**, select **Settings**, and select **Capture Windows Settings**.

### Variables for Capture Windows Settings

Use the following task sequence variables with this step:

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-output)
- [OSDMigrateComputerName](task-sequence-variables.md#OSDMigrateComputerName)
- [OSDMigrateRegistrationInfo](task-sequence-variables.md#OSDMigrateRegistrationInfo)
- [OSDMigrateTimeZone](task-sequence-variables.md#OSDMigrateTimeZone)
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-output)
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-output)

### Cmdlets for Capture Windows Settings

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Get-CMTSStepCaptureWindowsSettings)
- [New-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/New-CMTSStepCaptureWindowsSettings)
- [Remove-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Remove-CMTSStepCaptureWindowsSettings)
- [Set-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Set-CMTSStepCaptureWindowsSettings)

### Properties for Capture Windows Settings

On the **Properties** tab for this step, configure the settings described in this section.

#### Migrate computer name

Capture the NetBIOS computer name of the computer.

#### Migrate registered user and organization names

Capture the registered user and organization names from the computer.

#### Migrate time zone

Capture the time zone setting on the computer.


## <a name="BKMK_CheckReadiness"></a> Check Readiness

Use this step to verify that the target computer meets the specified deployment prerequisite conditions.

To add this step in the task sequence editor, select **Add**, select **General**, and select **Check Readiness**.

None of the following checks are selected by default in new or existing instances of the step.<!--6005561--> For more information on each check, see the specific sections below.

- **Architecture of current OS**
- **Minimum OS version**
- **Maximum OS version**
- **Minimum client version**
- **Language of current OS**
- **AC power plugged in**
- **Network adapter connected**
  - **Network adapter is not wireless**
- **Computer is in UEFI mode**<!--6452769-->

Starting in version 2103, the task sequence progress displays more information about readiness checks. If a task sequence fails because the client doesn't meet the requirements of this step, the user can select an option to **Inspect**. This action shows the checks that failed on the device. For more information, see [User experiences for OS deployment](user-experience.md#task-sequence-error).<!--8888218-->

Starting in version 2111, this step includes checks for TPM 2.0. These checks can help you better deploy Windows 11.<!-- 9575077 -->

> [!IMPORTANT]
> To take advantage of this new Configuration Manager feature, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

The **smsts.log** includes the outcome of all checks. If one check fails, the task sequence engine continues to evaluate the other checks. The step doesn't fail until all checks are complete. If at least one check fails, the step fails, and it returns error code **4316**. This error code translates to "The resource required for this operation does not exist."

### Variables for Check Readiness

Use the following task sequence variables with this step:

- [_TS_CRMEMORY](task-sequence-variables.md#TSCRMEMORY)
- [_TS_CRSPEED](task-sequence-variables.md#TSCRSPEED)
- [_TS_CRDISK](task-sequence-variables.md#TSCRDISK)
- [_TS_CROSTYPE](task-sequence-variables.md#TSCROSTYPE)
- [_TS_CRARCH](task-sequence-variables.md#TSCRARCH)
- [_TS_CRMINOSVER](task-sequence-variables.md#TSCRMINOSVER)
- [_TS_CRMAXOSVER](task-sequence-variables.md#TSCRMAXOSVER)
- [_TS_CRCLIENTMINVER](task-sequence-variables.md#TSCRCLIENTMINVER)
- [_TS_CROSLANGUAGE](task-sequence-variables.md#TSCROSLANGUAGE)
- [_TS_CRACPOWER](task-sequence-variables.md#TSCRACPOWER)
- [_TS_CRNETWORK](task-sequence-variables.md#TSCRNETWORK)
- [_TS_CRUEFI](task-sequence-variables.md#TSCRUEFI)
- [_TS_CRWIRED](task-sequence-variables.md#TSCRWIRED)
- [_TS_CRTPMACTIVATED](task-sequence-variables.md#TSCRTPMACTIVATED) (starting in version 2111)
- [_TS_CRTPMENABLED](task-sequence-variables.md#TSCRTPMENABLED) (starting in version 2111)

### Cmdlets for Check Readiness

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Get-CMTSStepPrestartCheck)
- [New-CMTSStepPrestartCheck](/powershell/module/configurationmanager/New-CMTSStepPrestartCheck)
- [Remove-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Remove-CMTSStepPrestartCheck)
- [Set-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Set-CMTSStepPrestartCheck)

### Properties for Check Readiness

On the **Properties** tab for this step, configure the settings described in this section.

#### Minimum memory (MB)

Verify that the amount of memory, in megabytes (MB), meets or exceeds the specified amount. The step enables this setting by default.

#### Minimum processor speed (MHz)

Verify that the speed of the processor, in megahertz (MHz), meets or exceeds the specified amount. The step enables this setting by default.

#### Minimum free disk space (MB)

Verify that the amount of free disk space, in megabytes (MB), meets or exceeds the specified amount.

Starting in version 2103, it also checks free space on disks without partitions.<!-- 8751864 -->

#### Current OS to be refreshed is

Verify that the OS installed on the target computer meets the specified requirement. The step sets this setting to **CLIENT** by default.

#### Architecture of current OS

Verify whether the current OS is **32-bit** or **64-bit**.

#### Minimum OS version

Verify that the current OS is running a version later than specified. Specify the version with major version, minor version, and build number. For example, `10.0.16299`.

#### Maximum OS version

Verify that the current OS is running a version earlier than specified. Specify the version with major version, minor version, and build number. For example, `10.0.18356`.

#### Minimum client version

Verify that the Configuration Manager client version is at least the specified version. Specify the client version in the following format: `5.00.8913.1005`.

#### Language of current OS

Verify that the current OS language matches what you specify. Select the language name, and the step compares the associated language code. This check compares the language that you select to the **OSLanguage** property of the **Win32_OperatingSystem** WMI class on the client.

#### AC power plugged in

Verify that the device is plugged in and not on battery.

#### Network adapter connected

Verify that the device has a network adapter that's connected to the network. You can also select the dependent check to verify that the **Network adapter is not wireless**.

#### Computer is in UEFI mode

Determine whether the device is configured for UEFI or BIOS.

#### TPM 2.0 or above is enabled

Starting in version 2111, checks whether the device that's running the task sequence has a TPM 2.0 that's enabled.<!--9575077-->

#### TPM 2.0 or above is activated

Starting in version 2111, if the device has an enabled TPM 2.0, check that it's activated.<!--9575077-->

### Options for Check Readiness

> [!NOTE]
> If you enable the **Continue on error** setting on the **Options** tab of this step, it only logs the readiness check results. If a check fails, the task sequence doesn't stop.



## <a name="BKMK_ConnectToNetworkFolder"></a> Connect To Network Folder

Use this step to create a connection to a shared network folder.

This task sequence step runs in the full OS or Windows PE.

To add this step in the task sequence editor, select **Add**, select **General**, and select **Connect To Network Folder**.

### Variables for Connect To Network Folder

Use the following task sequence variables with this step:

- [SMSConnectNetworkFolderAccount](task-sequence-variables.md#SMSConnectNetworkFolderAccount)
- [SMSConnectNetworkFolderDriveLetter](task-sequence-variables.md#SMSConnectNetworkFolderDriveLetter)
- [SMSConnectNetworkFolderPassword](task-sequence-variables.md#SMSConnectNetworkFolderPassword)
- [SMSConnectNetworkFolderPath](task-sequence-variables.md#SMSConnectNetworkFolderPath)

### Cmdlets for Connect To Network Folder

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Get-CMTSStepConnectNetworkFolder)
- [New-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/New-CMTSStepConnectNetworkFolder)
- [Remove-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Remove-CMTSStepConnectNetworkFolder)
- [Set-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Set-CMTSStepConnectNetworkFolder)

### Properties for Connect To Network Folder

On the **Properties** tab for this step, configure the settings described in this section.

#### Path

Select **Browse** to specify the network folder path. Use the format `\\server\share`.

#### Drive

Select the local drive letter to assign for this connection.

#### Account

Select **Set** to specify the user account with permissions to connect to this network folder. For more information on the task sequence network folder connection account, see [Accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account).



## <a name="BKMK_DisableBitLocker"></a> Disable BitLocker

Use this step to disable BitLocker encryption on the current OS drive, or on a specific drive. This action leaves the key protectors visible in clear text on the hard drive. It doesn't decrypt the contents of the drive. This action completes almost instantly.

> [!NOTE]
> BitLocker drive encryption provides low-level encryption of the contents of a disk volume.

If you have multiple encrypted drives, disable BitLocker on any data drives before disabling BitLocker on the OS drive.

This step runs only in the full OS. It doesn't run in Windows PE.

To add this step in the task sequence editor, select **Add**, select **Disks**, and select **Disable BitLocker**.

### Variables for Disable BitLocker

Use the following task sequence variables with this step:

- [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount)
- [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride)

### Cmdlets for Disable BitLocker

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepDisableBitLocker)
- [New-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/New-CMTSStepDisableBitLocker)
- [Remove-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepDisableBitLocker)
- [Set-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepDisableBitLocker)

### Properties for Disable BitLocker

On the **Properties** tab for this step, configure the settings described in this section.

#### Current operating system drive

Disables BitLocker on the current OS drive.

#### Specific drive

Disables BitLocker on a specific drive. Use the drop-down list to specify the drive where BitLocker is disabled.

#### Resume protection after Windows has been restarted the specified number of times

<!-- 4512937 -->
Use this option to specify the number of restarts to keep BitLocker disabled. Instead of adding multiple instances of this step, set a value between 1 (default) and 15.

You can set and modify this behavior with the task sequence variables [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount) and [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride).


## <a name="BKMK_DownloadPackageContent"></a> Download Package Content

Use this step to download any of the following package types:

- OS images
- OS upgrade packages
- Driver packages
- Packages
- Boot images <sup>[Note 1](#bkmk_note1)</sup>

This step works well in a task sequence to upgrade an OS in the following scenarios:

- To use a single upgrade task sequence that can work with both x86 and x64 platforms. Include two **Download Package Content** steps in the **Prepare for Upgrade** group. Specify conditions on the **Options** tab to detect the client architecture, and download only the appropriate OS upgrade package. Configure each **Download Package Content** step to use the same variable. Use the variable for the media path on the **Upgrade Operating System** step.

- To dynamically download an applicable driver package, use two **Download Package Content** steps with conditions to detect the appropriate hardware type for each driver package. Configure each **Download Package Content** step to use the same variable. Use the variable for the **Staged content** value in the Drivers section of the **Upgrade Operating System** step.

> [!NOTE]
> When you deploy a task sequence that contains this step, don't select **Download all content locally before starting the task sequence** or **Access content directly from a distribution point** for **Deployment options** on the **Distribution Points** page of the Deploy Software Wizard.

This step runs in either the full OS or Windows PE. The option to save the package in the Configuration Manager client cache isn't supported in Windows PE.

> [!NOTE]
> The **Download Package Content** task isn't supported for use with stand-alone media. For more information, see [Unsupported actions for stand-alone media](../deploy-use/create-stand-alone-media.md#unsupported-actions-for-stand-alone-media).

To add this step in the task sequence editor, select **Add**, select **Software**, and select **Download Package Content**.

### Cmdlets for Download Package Content

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Get-CMTSStepDownloadPackageContent)
- [New-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/New-CMTSStepDownloadPackageContent)
- [Remove-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Remove-CMTSStepDownloadPackageContent)
- [Set-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Set-CMTSStepDownloadPackageContent)

### Properties for Download Package Content

On the **Properties** tab for this step, configure the settings described in this section.

#### Select package

Select the icon to choose the package to download. After you choose one package, select the icon again to choose another package.

#### Place into the following location

Choose to save the package in one of the following locations:

- **Task sequence working directory**: This location is also referred to as the task sequence cache.

- **Configuration Manager client cache**: Use this option to store the content in the client cache. By default, this path is `%WinDir%\ccmcache`.

- **Custom path**: The task sequence engine first downloads the package to the task sequence working directory. It then moves the content to this path you specify. The task sequence engine appends the path with the package ID.

#### Save path as a variable

Save the package's path into a custom task sequence variable. Then use this variable in another task sequence step.

Configuration Manager adds a numerical suffix to the variable name. For example, you specify a variable of `%MyContent%` as a custom variable. It's the root for where the task sequence stores all referenced content for this step. This content may contain multiple packages. When you refer to the variable, add a numerical suffix. For the first package, refer to `%MyContent01%`. When you refer to the variable in subsequent steps, such as **Upgrade Operating System**, use `%MyContent02%` or `%MyContent03%`, where the number corresponds to the order that the **Download Package Content** step lists the packages.

#### If a package download fails, continue downloading other packages in the list

If the task sequence fails to download a package, it starts to download the next package in the list. This behavior applies to all packages in the step. The task sequence ignores download failures for any referenced package.

### <a name="bkmk_note1"></a> Note 1: Use of boot images in the Download Package Content step

<!-- SCCMDocs-pr #4202 -->

If you configure the [task sequence properties](../deploy-use/manage-task-sequences-to-automate-tasks.md#advanced-tab) to **Use a boot image**, then adding a boot image to this step is redundant. Only add a boot image to this step if it's not specified on the properties of the task sequence.

#### Example use case

- A single task sequence to pre-download content:
  - No associated boot image.
  - Runs only in the full OS, likely without user interaction.
  - Uses multiple **Download Package Content** steps with conditions. Depending upon the specific language and architecture, it downloads content to the client cache to prepare for the OS deployment task sequence.
  - There's only one instance of this task sequence, with all of the possible content options.

- Multiple OS deployment task sequences:
  - A normal OS deployment task sequence.
  - Has a boot image referenced in its properties.
  - There are multiple instances of this task sequence, with different boot images as needed by architecture and language

## Enable BitLocker

BitLocker drive encryption provides low-level encryption of the contents of a disk volume. Use this step to enable BitLocker encryption on at least two partitions on the hard drive. The first active partition contains the Windows bootstrap code. Another partition contains the OS. The bootstrap partition must remain unencrypted.

To enable BitLocker on a drive while in Windows PE, use the [Pre-provision BitLocker](#BKMK_PreProvisionBitLocker) step.

This step runs only in the full OS. It doesn't run in Windows PE.

To add this step in the task sequence editor, select **Add**, select **Disks**, and select **Enable BitLocker**.

When you specify **TPM Only**, **TPM and Startup Key on USB**, or **TPM and PIN**, the Trusted Platform Module (TPM) must be in the following state before you can run the **Enable BitLocker** step:

- Enabled
- Activated
- Ownership Allowed

You can skip this step for computers that don't have a TPM or when the TPM isn't enabled. This option makes it easier to manage the task sequence behavior on devices that can't fully support BitLocker.<!--6995601-->

This step completes any remaining TPM initialization. The remaining actions don't require physical presence or reboots. The **Enable BitLocker** step transparently completes the following remaining TPM initialization actions, if necessary:

- Create endorsement key pair
- Create owner authorization value and escrow the recovery information
- Take ownership
- Create the storage root key, or reset if already present but incompatible

If you want the task sequence to wait for the **Enable BitLocker** step to complete the drive encryption process, then select the **Wait** option. If you don't select the **Wait** option, the drive encryption process happens in the background. The task sequence immediately proceeds to the next step.

BitLocker can be used to encrypt multiple drives on a computer system, both OS and data drives. To encrypt a data drive, first encrypt the OS drive and complete the encryption process. This requirement is because the OS drive stores the key protectors for the data drives. If you encrypt the OS and data drives in the same task sequence, select the **Wait** option on the **Enable BitLocker** step for the OS drive.

If the hard drive is already encrypted, but BitLocker is disabled, then the **Enable BitLocker** step re-enables the key protectors and completes quickly. Re-encryption of the hard drive isn't necessary in this case.

### Variables for Enable BitLocker

Use the following task sequence variables with this step:

- [OSDBitLockerPIN](task-sequence-variables.md#osdbitlockerpin)
- [OSDBitLockerRecoveryPassword](task-sequence-variables.md#osdbitlockerrecoverypassword)
- [OSDBitLockerStartupKey](task-sequence-variables.md#osdbitlockerstartupkey)
- [OSDRecoveryKeyPollingFrequency](task-sequence-variables.md#osdrecoverykeypollingfrequency) _(starting in version 2203)_
- [OSDRecoveryKeyPollingTimeout](task-sequence-variables.md#osdrecoverykeypollingtimeout) _(starting in version 2203)_

### Cmdlets for Enable BitLocker

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepEnableBitLocker)
- [New-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/New-CMTSStepEnableBitLocker)
- [Remove-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepEnableBitLocker)
- [Set-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepEnableBitLocker)

### Properties for Enable BitLocker

On the **Properties** tab for this step, configure the settings described in this section.

#### Choose the drive to encrypt

Specifies the drive to encrypt. To encrypt the current OS drive, select **Current operating system drive**. Then configure one of the following options for key management:

- **TPM only**: Select this option to use only Trusted Platform Module (TPM).

- **Startup Key on USB only**: Select this option to use a startup key stored on a USB flash drive. When you select this option, BitLocker locks the normal boot process until a USB device that contains a BitLocker startup key is attached to the computer.

- **TPM and Startup Key on USB**: Select this option to use TPM and a startup key stored on a USB flash drive. When you select this option, BitLocker locks the normal boot process until a USB device that contains a BitLocker startup key is attached to the computer.

- **TPM and PIN**: Select this option to use TPM and a personal identification number (PIN). When you select this option, BitLocker locks the normal boot process until the user provides the PIN.

To encrypt a specific, non-OS data drive, select **Specific drive**. Then select the drive from the list.

#### Disk encryption mode

<!--6995601-->
Select one of the following encryption algorithms:

- AES_128
- AES_256
- XTS_AES256
- XTS_AES128

By default or if not specified, the step continues to use the default encryption method for the OS version. If the step runs on a version of Windows that doesn't support the specified algorithm, it falls back to the OS default. In this circumstance, the task sequence engine sends status message 11911.

#### Use full disk encryption

<!--SCCMDocs-pr issue 2671-->
By default, this step only encrypts used space on the drive. This default behavior is recommended, as it's faster and more efficient. If your organization requires encrypting the entire drive during setup, then enable this option. Windows Setup waits for the entire drive to encrypt, which takes a long time, especially on large drives.

> [!TIP]
> You can also use Configuration Manager to create and deploy BitLocker management policies. These policies use *full disk* encryption. To manage BitLocker on devices after the task sequence deploys the OS, enable this option. For more information, see [Plan for BitLocker management](../../protect/plan-design/bitlocker-management.md).

#### Choose where to create the recovery key

- **In Active Directory**: BitLocker creates the recovery password and escrows it in Active Directory. This option requires that you extend Active Directory for BitLocker key escrow. BitLocker can then save the associated recovery information in Active Directory.

- **The Configuration Manager database**: Starting in version 2203, escrow the BitLocker recovery information for the OS volume to Configuration Manager. Use this option if you deploy policies for [BitLocker management](../../protect/plan-design/bitlocker-management.md). Use this option instead of Active Directory or waiting for the Configuration Manager client to receive BitLocker management policy after the task sequence. By escrowing the recovery information to Configuration Manager during the task sequence, it makes sure that the device is fully protected by BitLocker when the task sequence completes. This behavior allows for you to immediately recover the OS volume.<!--10454717-->

  > [!NOTE]
  > The client will only escrow its key to the Configuration Manager site if you configure one of the following options:
  >
  > - Create and use a certificate to encrypt the site database for BitLocker management.
  >
  > - Enable the BitLocker client management policy option to **Allow recovery information to be stored in plain text**.
  >
  > For more information, see [Encrypt recovery data in the database](../../protect/deploy-use/bitlocker/encrypt-recovery-data.md).

To not create a password, select **Do not create recovery key** . Creating a password is the recommended option.

> [!NOTE]
> If Configuration Manager can't escrow the key, by default this task sequence step fails.

#### Wait for BitLocker to complete the drive encryption process on all drives before continuing task sequence execution

Select this option to allow BitLocker drive encryption to complete prior to running the next step in the task sequence. If you select this option, BitLocker encrypts the entire disk volume before the user is able to sign in to the computer.

The encryption process can take hours to complete when encrypting a large hard drive. Not selecting this option allows the task sequence to proceed immediately.

#### Skip this step for computers that do not have a TPM or when TPM is not enabled

<!--6995601-->
Select this option to skip drive encryption on a computer that doesn't contain a supported or enabled TPM. For example, use this option when you deploy an OS to a virtual machine. By default, this setting is disabled for the **Enable BitLocker** step. If you enable this setting, and the device doesn't have a functional TPM, the task sequence engine logs an error to smsts.log and sends status message 11912. The task sequence continues past this step.

## <a name="BKMK_FormatandPartitionDisk"></a> Format and Partition Disk

Use this step to format and partition a specified disk on the destination computer.

> [!IMPORTANT]
> Every setting you specify for this step applies to a single specified disk. To format and partition another disk on the destination computer, add an additional **Format and Partition Disk** step to the task sequence.

This step runs only in Windows PE. It doesn't run in the full OS.

To add this step in the task sequence editor, select **Add**, select **Disks**, and select **Format and Partition Disk**.

### Variables for Format and Partition Disk

Use the following task sequence variables with this step:

- [OSDDiskIndex](task-sequence-variables.md#OSDDiskIndex)
- [OSDGPTBootDisk](task-sequence-variables.md#OSDGPTBootDisk)
- [OSDPartitions](task-sequence-variables.md#OSDPartitions)
- [OSDPartitionStyle](task-sequence-variables.md#OSDPartitionStyle)

### Cmdlets for Format and Partition Disk

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPartitionDisk](/powershell/module/configurationmanager/get-cmtssteppartitiondisk)
- [New-CMTSStepPartitionDisk](/powershell/module/configurationmanager/new-cmtssteppartitiondisk)
- [Remove-CMTSStepPartitionDisk](/powershell/module/configurationmanager/remove-cmtssteppartitiondisk)
- [Set-CMTSStepPartitionDisk](/powershell/module/configurationmanager/set-cmtssteppartitiondisk)
- [New-CMTSPartitionSetting](/powershell/module/configurationmanager/new-cmtspartitionsetting)

### Properties for Format and Partition Disk

On the **Properties** tab for this step, configure the settings described in this section.

#### Disk Number

The physical disk number of the disk to format. The number is based on Windows disk enumeration ordering.

In version 2010 and earlier, this number can't be larger than 99. In version 2103 and later, the maximum number is 10,000. This change helps support storage area network (SAN) scenarios.<!-- 9528541 -->

#### Variable name to store disk number

<!--6610288-->

Use a task sequence variable to specify the target disk to format. This variable option supports more complex task sequences with dynamic behaviors. For example, a custom script can detect the disk and set the variable based on the hardware type. Then you can use multiple instances of this step to configure different hardware types and partitions.

If you select this property, enter a custom variable name. Add an earlier step in the task sequence to set the value of this custom variable to an integer value for the physical disk.

The following mock steps show one example:

- **Run PowerShell Script**: a custom script to collect target disks
  - Sets `myOSDisk` to `1`
  - Sets `myDataDisk` to `2`

- **Format and Partition Disk** for OS disk: specifies `myOSDisk` variable
  - Configures disk 1 as the system disk

- **Format and Partition Disk** for data disk: specifies `myDataDisk` variable
  - Configures disk 2 for raw storage

A variation of this example uses disk numbers and partitioning plans for different hardware types.

> [!NOTE]
> You can still use the existing task sequence variable **OSDDiskIndex**. However, each instance of the **Format and Partition Disk** step uses the same index value. If you want to programmatically set the disk number for multiple instances of this step, use this variable property.

#### Disk Type

The type of the disk to format. There are two options to select from the drop-down list:

- **Standard (MBR)**: Master Boot Record
- **GPT**: GUID Partition Table

> [!NOTE]
> If you change the disk type from **Standard (MBR)** to **GPT**, and the partition layout contains an extended partition, the task sequence removes all extended and logical partitions from the layout. The task sequence editor prompts to confirm this action before changing the disk type.

#### Volume

Specific information about the partition or volume that the task sequence creates, including the following attributes:

- Name
- Remaining disk space

To create a new partition, select **New** to launch the **Partition Properties** dialog box. Specify the partition type and size, and if it's a boot partition. To modify an existing partition, select the partition to be modified, and then select the **Properties** button. For more information about how to configure hard drive partitions, see one of the following articles:

- [UEFI/GPT-based hard drive partitions](/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)
- [BIOS/MBR-based hard drive partitions](/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)

To delete a partition, choose the partition, and then select **Delete**.



## <a name="BKMK_InstallApplication"></a> Install Application

This step installs the specified applications, or a set of applications defined by a dynamic list of task sequence variables. When the task sequence runs this step, the application installation begins immediately without waiting for a policy polling interval.

The applications must meet the following criteria:

- The application must have a deployment type of **Windows Installer** or **Script** installer. Windows app package (.appx, .appxbundle, .msix, .msixbundle file types) deployment types aren't supported.

- It must run under the Local System account and not the user account.

- It must not interact with the desktop. The program must run silently or in an unattended mode.

- It must not initiate a restart on its own. The application must request a restart by using the standard restart code, 3010. This behavior makes sure that this step correctly handles the restart. If the application returns a 3010 exit code, the task sequence engine restarts the computer. After the restart, the task sequence automatically continues.

- If the application [checks for running executable files](../../apps/deploy-use/check-for-running-executable-files.md), the task sequence will fail to install it. If you don't configure this step to continue on error, then the entire task sequence fails.

It's not supported to install applications during an OS deployment task sequence when the device also has policies assigned for [Windows Defender Application Control](../../protect/deploy-use/use-device-guard-with-configuration-manager.md). In this scenario, you can't use these applications after the task sequence completes. To work around this timing issue, [deploy the applications](../../apps/deploy-use/deploy-applications.md) after the task sequence completes.<!-- 13847501 -->

> [!NOTE]
> Starting in version 2107, when the following conditions are true, there's a seven-minute delay before this step:
>
> - The task sequence is running from standalone media.
> - The previous step was **Restart Computer**.
> - The current **Install Application** step doesn't _continue on error_.
>
> In versions 2103 and earlier, the step would fail under these conditions. The task sequence didn't properly evaluate that the app install was successful.<!-- 9849096 -->

When this step runs, the application checks the applicability of the requirement rules and detection method on its deployment types. Based on the results of this check, the application installs the applicable deployment type. If a deployment type contains dependencies, the dependent deployment type is evaluated and installed as part of this step. Application dependencies aren't supported for stand-alone media.

> [!NOTE]
> To install an application that supersedes another application, the content files for the superseded application must be available. Otherwise this task sequence step fails. For example, Microsoft Visio 2010 is installed on a client or in a captured image. When the **Install Application** step installs Microsoft Visio 2013, the content files for Microsoft Visio 2010 (the superseded application) must be available on a distribution point. If Microsoft Visio isn't installed at all on a client or captured image, the task sequence installs Microsoft Visio 2013 without checking for the Microsoft Visio 2010 content files.
>
> If you retire a superseded app, and the new app is referenced in a task sequence, the task sequence fails to start.
This behavior is by design: the task sequence requires all app references.<!-- SCCMDocs 1711 -->

This task sequence step runs only in the full OS. It doesn't run in Windows PE.

To add this step in the task sequence editor, select **Add**, select **Software**, and select **Install Application**.

### Variables for Install Application

Use the following task sequence variables with this step:

- [_TSAppInstallStatus](task-sequence-variables.md#TSAppInstallStatus)
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)
- [TSErrorOnWarning](task-sequence-variables.md#TSErrorOnWarning)

> [!NOTE]
> If the client fails to retrieve the management point list from location services, use the **SMSTSMPListRequestTimeoutEnabled** and **SMSTSMPListRequestTimeout** task sequence variables. These variables specify how many milliseconds a task sequence waits before it retries installing an application. For more information, see [Task sequence variables](task-sequence-variables.md).

### Cmdlets for Install Application

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallApplication](/powershell/module/configurationmanager/get-cmtsstepinstallapplication)
- [New-CMTSStepInstallApplication](/powershell/module/configurationmanager/new-cmtsstepinstallapplication)
- [Remove-CMTSStepInstallApplication](/powershell/module/configurationmanager/remove-cmtsstepinstallapplication)
- [Set-CMTSStepInstallApplication](/powershell/module/configurationmanager/set-cmtsstepinstallapplication)

### Properties for Install Application

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
> You can't install applications by using a dynamic variable list for stand-alone media deployments.

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

#### Clear application content from cache after installing

<!--4485675-->
Delete the app content from the client cache after the step runs. This behavior is beneficial on devices with small hard drives or when installing lots of large apps in succession.


### Options for Install Application

> [!NOTE]
> When you select **Continue on error** on the **Options** tab of this step, the task sequence continues when an application fails to install. When you don't enable this option, the task sequence fails, and doesn't install remaining applications.

Besides the default options, configure the following additional settings on the **Options** tab of this task sequence step:

#### Retry this step if computer unexpectedly restarts

If one of the application installations unexpectedly restarts the computer, retry this step. The step enables this setting by default with two retries. You can specify from one to five retries.



## <a name="BKMK_InstallPackage"></a> Install Package

Use this step to install a software package as part of the task sequence. When this step runs, the installation begins immediately without waiting for a policy polling interval.

The package must meet the following criteria:

- It must run under the Local System account and not a user account.

- It shouldn't interact with the desktop. The program must run silently or in an unattended mode.

- It must not initiate a restart on its own. The software must request a restart using the standard restart code, 3010. This behavior makes sure that the task sequence properly handles the restart. If the software does return a 3010 exit code, the task sequence engine restarts the computer. After the restart, the task sequence automatically continues.

Programs that use the **Run another program first** option to install a dependent program aren't supported when deploying an OS. If you enable the package option **Run another program first**, and the dependent program already ran on the destination computer, the dependent program runs and the task sequence continues. However, if the dependent program hasn't already run on the destination computer, the task sequence step fails.

This task sequence step runs only in the full OS. It doesn't run in Windows PE.

To add this step in the task sequence editor, select **Add**, select **Software**, and select **Install Package**.

#### Known issue with Install Package step and standalone media created at the central administration site

An error might occur if your task sequence includes the [Install Package](../understand/task-sequence-steps.md#BKMK_InstallPackage) step and you create the stand-alone media at a central administration site (CAS). The CAS doesn't have the necessary client configuration policies. These policies are required to enable the software distribution agent when the task sequence runs. The following error might appear in the **CreateTsMedia.log** file: `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`

For stand-alone media that includes an **Install Package** step, create the stand-alone media at a primary site that has the software distribution agent enabled.

Alternatively, use a custom [Run PowerShell Script](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript) step. Add it after the [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) step and before the first **Install Package** step. The **Run PowerShell Script** step runs the following commands to enable the software distribution agent before the first Install Package step:

```powershell
$namespace = "root\ccm\policy\machine\requestedconfig"
$class = "CCM_SoftwareDistributionClientConfig"
$classArgs = @{
    ComponentName = 'Enable SWDist'
    Enabled = 'true'
    LockSettings='TRUE'
    PolicySource='local'
    PolicyVersion='1.0'
    SiteSettingsKey='1'
}
Set-WmiInstance -Namespace $namespace -Class $class -Arguments $classArgs -PutType CreateOnly
```

### Variables for Install Package

Use the following task sequence variables with this step:

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) <!--1358493-->

### Cmdlets for Install Package

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallSoftware](/powershell/module/configurationmanager/get-cmtsstepinstallsoftware)
- [New-CMTSStepInstallSoftware](/powershell/module/configurationmanager/new-cmtsstepinstallsoftware)
- [Remove-CMTSStepInstallSoftware](/powershell/module/configurationmanager/remove-cmtsstepinstallsoftware)
- [Set-CMTSStepInstallSoftware](/powershell/module/configurationmanager/set-cmtsstepinstallsoftware)

> [!TIP]
> Use content pre-caching to download an applicable OS upgrade package before a user installs the task sequence. For more information, see [Configure pre-cache content](../deploy-use/configure-precache-content.md).

### Properties for Install Package

On the **Properties** tab for this step, configure the settings described in this section.

#### Install a single software package

This setting specifies a Configuration Manager software package. The step waits until the installation completes.

#### Install software packages according to dynamic variable list

The task sequence installs packages using this base variable name. The base variable name is for a set of task sequence variables defined for a collection or computer. These variables specify the packages that the task sequence installs for that collection or computer. Each variable name consists of its common base name plus a numerical suffix starting at 001. The value for each variable must contain a package ID and the name of the software separated by a colon.

For the task sequence to install software by using a dynamic variable list, enable the following setting on the **Advanced** tab of the package **Properties**: **Allow this program to be installed from the Install Package task sequence without being deployed**.

> [!NOTE]
> You can't install software packages by using a dynamic variable list for stand-alone media deployments.

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

#### Retry this step if computer unexpectedly restarts

If one of the package installations unexpectedly restarts the computer, retry this step. The step enables this setting by default with two retries. You can specify from one to five retries. <!--24334765-->


## <a name="BKMK_InstallSoftwareUpdates"></a> Install Software Updates

Use this step to install software updates on the destination computer. The destination computer isn't evaluated for applicable software updates until this task sequence step runs. At that time, the destination computer is evaluated for software updates like any other Configuration Manager client. For this step to install software updates, first deploy the updates to a collection of which the target computer is a member.

> [!IMPORTANT]
> For best performance, install the latest version of the Windows Update Agent.

This task sequence step runs only in the full OS. It doesn't run in Windows PE.

To add this step in the task sequence editor, select **Add**, select **Software**, and select **Install Software Updates**.

### Variables for Install Software Updates

Use the following task sequence variables with this step:

- [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget)
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)
- [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)
- [SMSTSWaitForSecondReboot](task-sequence-variables.md#SMSTSWaitForSecondReboot)

> [!NOTE]
> If the client fails to retrieve the management point list from location services, use the **SMSTSMPListRequestTimeoutEnabled** and **SMSTSMPListRequestTimeout** variables. These variables specify how many milliseconds a task sequence waits before it retries installing an application or software update. For more information, see [Task sequence variables](task-sequence-variables.md).

### Cmdlets for Install Software Updates

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallUpdate](/powershell/module/configurationmanager/get-cmtsstepinstallupdate)
- [New-CMTSStepInstallUpdate](/powershell/module/configurationmanager/new-cmtsstepinstallupdate)
- [Remove-CMTSStepInstallUpdate](/powershell/module/configurationmanager/remove-cmtsstepinstallupdate)
- [Set-CMTSStepInstallUpdate](/powershell/module/configurationmanager/set-cmtsstepinstallupdate)

For more recommendations and a technical flow chart diagram for this step, see [Install Software Updates](install-software-updates.md).

### Properties for Install Software Updates

On the **Properties** tab for this step, configure the settings described in this section.

#### Required for installation - Mandatory software updates only

Select this option to install all mandatory software updates with administrator-defined installation deadlines.

#### Available for installation - All software updates

Select this option to install all available software updates. First deploy these updates to a collection of which the computer is a member. The task sequence installs all available software updates on the destination computers.

#### Evaluate software updates from cached scan results

By default, this step uses cached scan results from the Windows Update Agent. Disable this option to instruct the Windows Update Agent to download the latest catalog from the software update point. Enable this option when using a task sequence to [capture and build an OS image](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).

Many updates have dependencies. For example, install update ABC before update XYZ appears as applicable. When you disable this setting, and deploy the task sequence to many clients, they all connect to the software update point at the same time. This behavior might result in performance issues during the process and download of the update catalog. If deploying to many clients at once, use the default setting to use cached scan results. If deploying to a small number of clients at once, uncheck this option to ensure all software updates are installed on the client.

The **SMSTSSoftwareUpdateScanTimeout** variable controls the software updates scan timeout during this step. The default value is 60 minutes. For more information, see [Task sequence variables](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout).

### Options for Install Software Updates

Besides the default options, configure the following additional settings on the **Options** tab of this task sequence step:

#### Retry this step if computer unexpectedly restarts

If one of the updates unexpectedly restarts the computer, retry this step. The step enables this setting by default with two retries. You can specify from one to five retries.

This option only applies to stand-alone task sequences. It doesn't work with OSD task sequences that deploy an OS and utilize the **Setup Windows and ConfigMgr** task. For OSD task sequences that deploy an OS and utilize the **Setup Windows and ConfigMgr** task, use the **SMSTSWaitForSecondReboot** variable instead. For more information, see [Task sequence variables: SMSTSWaitForSecondReboot](task-sequence-variables.md#SMSTSWaitForSecondReboot).



## <a name="BKMK_JoinDomainorWorkgroup"></a> Join Domain or Workgroup

Use this step to add the destination computer to a workgroup or domain.

> [!NOTE]
> When a Microsoft Entra joined client runs an OS deployment task sequence, the client in the new OS won't automatically join Microsoft Entra ID. Even though it's not Microsoft Entra joined, the client is still managed.

This task sequence step runs only in the full OS. It doesn't run in Windows PE.

To add this step in the task sequence editor, select **Add**, select **General**, and select **Join Domain or Workgroup**.

### Variables for Join Domain or Workgroup

Use the following task sequence variables with this step:

- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)
- [OSDJoinDomainName](task-sequence-variables.md#OSDJoinDomainName)
- [OSDJoinDomainOUName](task-sequence-variables.md#OSDJoinDomainOUName)
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)
- [OSDJoinSkipReboot](task-sequence-variables.md#OSDJoinSkipReboot)
- [OSDJoinType](task-sequence-variables.md#OSDJoinType)
- [OSDJoinWorkgroupName](task-sequence-variables.md#OSDJoinWorkgroupName)

### Cmdlets for Join Domain or Workgroup

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Get-CMTSStepJoinDomainWorkgroup)
- [New-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/New-CMTSStepJoinDomainWorkgroup)
- [Remove-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Remove-CMTSStepJoinDomainWorkgroup)
- [Set-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Set-CMTSStepJoinDomainWorkgroup)

### Properties for Join Domain or Workgroup

On the **Properties** tab for this step, configure the settings described in this section.

#### Join a workgroup

Select this option to have the destination computer join the specified workgroup. If the computer is currently a member of a domain, selecting this option causes the computer to reboot.

#### Join a domain

Select this option to have the destination computer join the specified domain.

Optionally, enter or browse for an organizational unit (OU) in the specified domain for the computer to join. If the computer is currently a member of some other domain or a workgroup, this option causes the computer to reboot. If the computer is already a member of another OU, since Active Directory Domain Services doesn't allow changing the OU via this method, Windows Setup ignores this setting.

#### Enter the account which has permission to join the domain

Select **Set** to enter the username and password for an account with permissions to join the domain. Enter the account in the format:  `Domain\account`. For more information on the task sequence domain joining account, see [Accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Prepare ConfigMgr Client for Capture

Use this step to remove or configure the Configuration Manager client on the reference computer. This action prepares the computer for capture as part of the imaging process.

This step completely removes the Configuration Manager client, instead of only removing key information. When the task sequence deploys the captured OS image, it installs a new Configuration Manager client each time.

> [!TIP]
> By default, the task sequence engine only removes the client during the **Build and capture a reference operating system image** task sequence. The task sequence engine doesn't remove the client during other capture methods, such as capture media or a custom task sequence. You can override this behavior for an OS deployment task sequence. Set the task sequence variable **SMSTSUninstallCCMClient** to **TRUE** before the **Prepare ConfigMgr Client for Capture** step. This variable and behavior only apply to OS deployment task sequences. It removes the client after the next restart of the device.

This task sequence step runs only in the full OS. It doesn't run in Windows PE.

To add this step in the task sequence editor, select **Add**, select **Images**, and select **Prepare ConfigMgr Client for Capture**.


### Variables for Prepare ConfigMgr Client for Capture

Use the following task sequence variables with this step:

- SMSTSUninstallCCMClient


### Cmdlets for Prepare ConfigMgr Client for Capture

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Get-CMTSStepPrepareConfigMgrClient)
- [New-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/New-CMTSStepPrepareConfigMgrClient)
- [Remove-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Remove-CMTSStepPrepareConfigMgrClient)
- [Set-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Set-CMTSStepPrepareConfigMgrClient)

## <a name="BKMK_PrepareWindowsforCapture"></a> Prepare Windows for Capture

Use this step to specify the Sysprep options when capturing an OS image on the reference computer. This step runs Sysprep, and then reboots the computer into the Windows PE boot image specified for the task sequence. This action fails if the reference computer is joined to a domain.

This step runs only in the full OS. It doesn't run in Windows PE.

To add this step in the task sequence editor, select **Add**, select **Images**, and select **Prepare Windows for Capture**.

### Variables for Prepare Windows for Capture

Use the following task sequence variables with this step:

- [OSDKeepActivation](task-sequence-variables.md#OSDKeepActivation)
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-output)

### Cmdlets for Prepare Windows for Capture

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Get-CMTSStepPrepareWindows)
- [New-CMTSStepPrepareWindows](/powershell/module/configurationmanager/New-CMTSStepPrepareWindows)
- [Remove-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Remove-CMTSStepPrepareWindows)
- [Set-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Set-CMTSStepPrepareWindows)

### Properties for Prepare Windows for Capture

On the **Properties** tab for this step, configure the settings described in this section.

#### Automatically build mass storage driver list

Select this option to have Sysprep automatically build a list of mass storage drivers from the reference computer. This option enables the Build Mass Storage Drivers option in the sysprep.inf file on the reference computer. For more information about this setting, see the Sysprep documentation.

> [!IMPORTANT]
>
> This option was only applicable in Windows XP. It's no longer applicable in any currently supported versions of Windows.

#### Do not reset activation flag

Select this option to prevent Sysprep from resetting the product activation flag.

#### Shut down the computer after running this action

<!--SCCMDocs-pr issue 2695-->
This option instructs Sysprep to shutdown the computer instead of its default restart behavior.

The [Windows Autopilot for existing devices](/autopilot/existing-devices) task sequence uses this step with this option.

- If you want the task sequence to refresh the device and then immediately start OOBE for Autopilot, leave this option off.

- Enable this option to shut down the device after imaging. Then you can deliver the device to a user, who starts OOBE with Autopilot when they turn it on for the first time.

> [!IMPORTANT]
>
> Don't use the **Prepare Windows for Capture** task with **Windows Autopilot for existing devices** task sequences. The `Sysprep.exe` command line used during the **Prepare Windows for Capture** task uses the `/Generalize` parameter. The `/Generalize` parameter removes the `AutopilotConfigurationFile.json` file used by Windows Autopilot, causing the Windows Autopilot deployment not to run during the out-of-box (OOBE) experience. Instead, where the **Prepare Windows for Capture** task normally runs, add a **Run Command Line** task that runs the following `Sysprep.exe` command instead:
>
> ```cmd
> C:\Windows\System32\sysprep\sysprep.exe /oobe /reboot
> ```
>
> For more information, see [Modify the task sequence to account for Sysprep command line configuration](/autopilot/tutorial/existing-devices/create-autopilot-task-sequence#modify-the-task-sequence-to-account-for-sysprep-command-line-configuration) and [Windows Autopilot for existing devices doesn't work](/autopilot/known-issues#windows-autopilot-for-existing-devices-doesnt-work).

## <a name="BKMK_PreProvisionBitLocker"></a> Pre-provision BitLocker

Use this step to enable BitLocker on a drive while in Windows PE. By default, only the used drive space is encrypted, so encryption times are much faster. You apply the key management options by using the [Enable BitLocker](#enable-bitlocker) step after the OS installs.

> [!IMPORTANT]
> Pre-provisioning BitLocker requires that the computer has a supported and enabled Trusted Platform Module (TPM).

This step runs only in Windows PE. It doesn't run in the full OS.

To add this step in the task sequence editor, select **Add**, select **Disks**, and select **Pre-provision BitLocker**.

### Cmdlets for Pre-provision BitLocker

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepOfflineEnableBitLocker)
- [New-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/New-CMTSStepOfflineEnableBitLocker)
- [Remove-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepOfflineEnableBitLocker)
- [Set-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepOfflineEnableBitLocker)

### Properties for Pre-provision BitLocker

On the **Properties** tab for this step, configure the settings described in this section.

#### Apply BitLocker to the specified drive

Specify the drive for which you want to enable BitLocker. BitLocker only encrypts the used space on the drive.

#### Disk encryption mode (Pre-provision BitLocker)

<!--6995601-->
Select one of the following encryption algorithms:

- AES_128
- AES_256
- XTS_AES256
- XTS_AES128

By default or if not specified, the step continues to use the default encryption method for the OS version. If the step runs on a version of Windows that doesn't support the specified algorithm, it falls back to the OS default. In this circumstance, the task sequence engine sends status message 11911.

#### Use full disk encryption (Pre-provision BitLocker)

<!--SCCMDocs-pr issue 2671-->
By default, this step only encrypts used space on the drive. This default behavior is recommended, as it's faster and more efficient. If your organization requires encrypting the entire drive during setup, then enable this option. Windows Setup waits for the entire drive to encrypt, which takes a long time, especially on large drives.

#### Skip this step for computers that do not have a TPM or when TPM is not enabled (Pre-provision BitLocker)

Select this option to skip drive encryption on a computer that doesn't contain a supported or enabled TPM. For example, use this option when you deploy an OS to a virtual machine. By default, this setting is enabled for the **Pre-provision BitLocker** step. The step fails on a device without a TPM or a TPM that doesn't initialize. If the device doesn't have a functional TPM, the task sequence engine logs a warning to smsts.log and sends status message 11912.

## <a name="BKMK_ReleaseStateStore"></a> Release State Store

Use this step to notify the state migration point that the capture or restore action is complete. Use this step in conjunction with the **Request State Store**, **Capture User State**, and **Restore User State** steps. You use these steps to migrate user state data using a state migration point and the User State Migration Tool (USMT).

For more information about managing the user state when deploying operating systems, see [Manage user state](../get-started/manage-user-state.md).

If you use the **Request State Store** step to request access to a state migration point to *capture* user state, this step notifies the state migration point that the capture process is complete. The state migration point then marks the user state data as available for restore. The state migration point sets the access control permissions for the user state data so that only the restoring computer has read-only access.

If you use the **Request State Store** step to request access to a state migration point to *restore* user state, this step notifies the state migration point that the restore process is complete. The state migration point then activates its configured data retention settings.

> [!IMPORTANT]
> Set the **Continue on Error** option for any steps between the **Request State Store** and **Release State Store** steps. Every **Request State Store** step must have a matching **Release State Store** step.

This step runs only in the full OS. It doesn't run in Windows PE.

To add this step in the task sequence editor, select **Add**, select **User State**, and select **Release State Store**.

### Variables for Release State Store

Use the following task sequence variables with this step:

- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)

### Cmdlets for Release State Store

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Get-CMTSStepReleaseStateStore)
- [New-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/New-CMTSStepReleaseStateStore)
- [Remove-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Remove-CMTSStepReleaseStateStore)
- [Set-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Set-CMTSStepReleaseStateStore)

### Properties for Release State Store

This step doesn't require any settings on the **Properties** tab.



## <a name="BKMK_RequestStateStore"></a> Request State Store

Use this step to request access to a state migration point when capturing or restoring state.

For more information about managing the user state when deploying operating systems, see [Manage user state](../get-started/manage-user-state.md).

Use this step in conjunction with the **Release State Store**, **Capture User State**, and **Restore User State** steps. You use these steps to migrate computer state using a state migration point and the User State Migration Tool (USMT).

> [!NOTE]
> When creating a new state migration point, user state storage isn't available for up to one hour. To expedite availability, adjust any property settings on the state migration point to trigger a site control file update.

This step runs in the full OS and in Windows PE for offline USMT.

To add this step in the task sequence editor, select **Add**, select **User State**, and select **Request State Store**.

### Variables for Request State Store

Use the following task sequence variables with this step:

- [OSDStateFallbackToNAA](task-sequence-variables.md#OSDStateFallbackToNAA)
- [OSDStateSMPRetryCount](task-sequence-variables.md#OSDStateSMPRetryCount)
- [OSDStateSMPRetryTime](task-sequence-variables.md#OSDStateSMPRetryTime)
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)

### Cmdlets for Request State Store

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Get-CMTSStepRequestStateStore)
- [New-CMTSStepRequestStateStore](/powershell/module/configurationmanager/New-CMTSStepRequestStateStore)
- [Remove-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Remove-CMTSStepRequestStateStore)
- [Set-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Set-CMTSStepRequestStateStore)

### Properties for Request State Store

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



## <a name="BKMK_RestartComputer"></a> Restart Computer

Use this step to restart the computer running the task sequence. After the restart, the computer automatically continues with the next step in the task sequence.

This step can be run in either the full OS or Windows PE.

To add this step in the task sequence editor, select **Add**, select **General**, and select **Restart Computer**.

### Variables for Restart Computer

Use the following task sequence variables with this step:

- [SMSRebootMessage](task-sequence-variables.md#SMSRebootMessage)
- [SMSRebootTimeout](task-sequence-variables.md#SMSRebootTimeout)

### Cmdlets for Restart Computer

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReboot](/powershell/module/configurationmanager/get-cmtsstepreboot)
- [New-CMTSStepReboot](/powershell/module/configurationmanager/new-cmtsstepreboot)
- [Remove-CMTSStepReboot](/powershell/module/configurationmanager/remove-cmtsstepreboot)
- [Set-CMTSStepReboot](/powershell/module/configurationmanager/set-cmtsstepreboot)

### Properties for Restart Computer

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



## <a name="BKMK_RestoreUserState"></a> Restore User State

Use this step to initiate the User State Migration Tool (USMT) to restore user state and settings to the destination computer. You use this step in conjunction with the **Capture User State** step.

For more information about managing the user state when deploying operating systems, see [Manage user state](../get-started/manage-user-state.md).

Use this step with the **Request State Store** and **Release State Store** steps to save or restore the state settings with a state migration point. This option always decrypts the USMT state store by using an encryption key that Configuration Manager generates and manages.

Starting in version 2103, this step and the **Capture User State** step use the current highest supported encryption algorithm, **AES 256**.<!--9171505-->

> [!IMPORTANT]
> If you have any active user state migrations, before you update the Configuration Manager client on those devices, restore the user state. Otherwise, the updated client will fail to restore the user state when it tries to use a different encryption algorithm. If necessary, you can manually restore the user state and explicitly use the USMT parameter `/decrypt:3DES`.

The **Restore User State** step provides control over a limited subset of the most commonly used USMT options. Specify additional command-line options with the **OSDMigrateAdditionalRestoreOptions** variable.

> [!IMPORTANT]
> If you're using this step for a purpose unrelated to an OS deployment scenario, add the [Restart Computer](#BKMK_RestartComputer) step immediately following the **Restore User State** step.

This step runs only in the full OS. It doesn't run in Windows PE.

To add this step in the task sequence editor, select **Add**, select **User State**, and select **Restore User State**.

### Variables for Restore User State

Use the following task sequence variables with this step:

- [_OSDMigrateUsmtRestorePackageID](task-sequence-variables.md#OSDMigrateUsmtRestorePackageID)
- [OSDMigrateAdditionalRestoreOptions](task-sequence-variables.md#OSDMigrateAdditionalRestoreOptions)
- [OSDMigrateContinueOnRestore](task-sequence-variables.md#OSDMigrateContinueOnRestore)
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)
- [OSDMigrateLocalAccounts](task-sequence-variables.md#OSDMigrateLocalAccounts)
- [OSDMigrateLocalAccountPassword](task-sequence-variables.md#OSDMigrateLocalAccountPassword)
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)

### Cmdlets for Restore User State

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Get-CMTSStepRestoreUserState)
- [New-CMTSStepRestoreUserState](/powershell/module/configurationmanager/New-CMTSStepRestoreUserState)
- [Remove-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Remove-CMTSStepRestoreUserState)
- [Set-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Set-CMTSStepRestoreUserState)

### Properties for Restore User State

On the **Properties** tab for this step, configure the settings described in this section.

#### User state migration tool package

Specify the package that contains the version of USMT for this step to use. This package doesn't require a program. When the step runs, the task sequence uses the version of USMT in the specified package. Specify a package containing the 32-bit or 64-bit version of USMT. The architecture of USMT depends upon the architecture of the OS to which the task sequence is restoring state.

#### Restore all captured user profiles with standard options

Restores the captured user profiles with the standard options. To customize the options that USMT restores, select **Customize user profile capture**.

#### Customize how user profiles are restored

Allows you to customize the files that you want to restore to the destination computer. Select **Files** to specify the configuration files in the USMT package you want to use for restoring the user profiles. To add a configuration file, enter the name of the file in the **Filename** box, and then select **Add**. The Files pane lists the configuration files that USMT uses. The .xml file you specify defines which user file USMT restores.

#### Restore local computer user profiles

Restores the local computer user profiles. These profiles aren't for domain users. Assign new passwords to the restored local user accounts. USMT can't migrate the original passwords. Enter the new password in the **Password** box, and confirm the password in the **Confirm Password** box.

#### Continue if some files cannot be restored

Continues restoring user state and settings even if USMT is unable to restore some files. The step enables this option by default. If you disable this option, and USMT encounters errors while restoring files, this step fails immediately. USMT doesn't restore all files.

#### Enable verbose logging

Enable this option to generate more detailed log file information. When restoring state, the task sequence by default generates **Loadstate.log** in the task sequence log folder, `%WinDir%\ccm\logs`.



## <a name="BKMK_RunCommandLine"></a> Run Command Line

Use this step to run the specified command line.

The command being run must meet the following criteria:

- It shouldn't interact with the desktop. The command must run silently or in an unattended mode.

- It must not initiate a restart on its own. The command must request a restart using the standard restart code, 3010. This behavior makes sure that the task sequence properly handles the restart. If the command does return a 3010 exit code, the task sequence engine restarts the computer. After the restart, the task sequence automatically continues.

This step can be run in the full OS or Windows PE.

To add this step in the task sequence editor, select **Add**, select **General**, and select **Run Command Line**.

### Variables for Run Command Line

Use the following task sequence variables with this step:

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand)<!--3654172-->
- [SMSTSDisableWow64Redirection](task-sequence-variables.md#SMSTSDisableWow64Redirection)
- [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName)
- [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword)
- [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser)<!-- 5573175 -->
- [WorkingDirectory](task-sequence-variables.md#WorkingDirectory)

### Cmdlets for Run Command Line

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunCommandLine](/powershell/module/configurationmanager/get-cmtsstepruncommandline)
- [New-CMTSStepRunCommandLine](/powershell/module/configurationmanager/new-cmtsstepruncommandline)
- [Remove-CMTSStepRunCommandLine](/powershell/module/configurationmanager/remove-cmtsstepruncommandline)
- [Set-CMTSStepRunCommandLine](/powershell/module/configurationmanager/set-cmtsstepruncommandline)

### Properties for Run Command Line

On the **Properties** tab for this step, configure the settings described in this section.

#### Command line

Specifies the command line that the task sequence runs. This field is required. Include file name extensions, for example, .vbs and .exe. Include all required settings files and command-line options.

If you don't specify the file name extension, Configuration Manager tries .com, .exe, and .bat. If the file name has an extension that's not an executable type, Configuration Manager tries to apply a local association. For example, if the command line is readme.gif, Configuration Manager starts the application specified on the destination computer for opening .gif files.

Examples:

`setup.exe /a`

`cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`

> [!NOTE]
> To run successfully, precede command-line actions with the **cmd.exe /c** command. Example of these actions include output redirection, piping, and copy commands.

#### Output to task sequence variable

<!--user story 4977616/bug 4798352-->

Use this setting to save the command output to a custom task sequence variable.

> [!NOTE]
> Configuration Manager limits this output to the last 1000 characters.

#### Disable 64-bit file system redirection

By default, 64-bit operating systems use the WOW64 file system redirector to run command lines. This behavior is to properly find 32-bit versions of OS executables and libraries. Select this option to disable the use of the WOW64 file system redirector. Windows runs the command using native 64-bit versions of OS executables and libraries. This option has no effect when running on a 32-bit OS.

#### Start in

Specifies the executable folder for the program, up to 127 characters. This folder can be an absolute path on the destination computer or a path relative to the distribution point folder that contains the package. This field is optional.

Examples:

`c:\officexp`

`i386`

> [!NOTE]
> The **Browse** button browses the local computer for files and folders. Anything you select must also exist on the destination computer. It must exist in the same location and with the same file and folder names.

#### Package

When you specify files or programs on the command line that aren't already present on the destination computer, select this option to specify the Configuration Manager package that contains the necessary files. The package doesn't require a program. If the specified files exist on the destination computer, this option isn't required.

#### Time-out

Specifies a value that represents how long Configuration Manager allows the command line to run. This value can be from one minute to 999 minutes. The default value is 15 minutes. This option is disabled by default.

> [!IMPORTANT]
> If you enter a value that doesn't allow enough time for the specified command to complete successfully, this step fails. The entire task sequence could fail depending on step or group conditions. If the time-out expires, Configuration Manager terminates the command-line process.

#### Run this step as the following account

Specifies that the command line is run as a Windows user account other than the Local System account.

> [!NOTE]
> To run simple scripts or commands with another account after installing the OS, first add the account to the computer. Additionally, you may need to restore Windows user profiles to run more complex programs, such as a Windows Installer.

#### Account

Specifies the Windows user account this step uses to run the command line. The command line runs with the permissions of the specified account. Select **Set** to specify the local user or domain account. For more information on the task sequence run-as account, see [Accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

> [!IMPORTANT]
> If this step specifies a user account and runs in Windows PE, the action fails. You can't join Windows PE to a domain. The **smsts.log** file records this failure.

### Options for Run Command Line

Besides the default options, configure the following additional settings on the **Options** tab of this task sequence step:

#### Success codes

Include other exit codes from the script that the step should evaluate as success.



## <a name="BKMK_RunPowerShellScript"></a> Run PowerShell Script

Use this step to run the specified Windows PowerShell script.

The script must meet the following criteria:

- It shouldn't interact with the desktop. The script must run silently or in an unattended mode.

- It must not initiate a restart on its own. The script must request a restart using the standard restart code, 3010. This behavior makes sure that the task sequence properly handles the restart. If the script does return a 3010 exit code, the task sequence engine restarts the computer. After the restart, the task sequence automatically continues.

- Use signed PowerShell scripts in Unicode format. ANSI format, which is the default, doesn't work with this step.

This step can be run in the full OS or Windows PE. To run this step in Windows PE, enable PowerShell in the boot image. Enable the WinPE-PowerShell component from the **Optional Components** tab in the properties for the boot image. For more information about how to modify a boot image, see [Manage boot images](../get-started/manage-boot-images.md).

> [!NOTE]
> PowerShell isn't enabled by default on Windows Embedded operating systems.

> [!WARNING]
> Some antimalware software may inadvertently trigger events for this task sequence step. To allow these scripts to run without interference, configure the antimalware software to exclude `%windir%\temp\smstspowershellscripts`.

To add this step in the task sequence editor, select **Add**, select **General**, and select **Run PowerShell Script**.

### Variables for Run PowerShell Script

Use the following task sequence variables with this step:

- [OSDLogPowerShellParameters](task-sequence-variables.md#OSDLogPowerShellParameters)<!--3556028-->
- [SMSTSRunPowerShellAsUser](task-sequence-variables.md#SMSTSRunPowerShellAsUser)<!-- 5573175 -->
- [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName)
- [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword)

### Cmdlets for Run PowerShell Script

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/get-cmtssteprunpowershellscript)
- [New-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/new-cmtssteprunpowershellscript)
- [Remove-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/remove-cmtssteprunpowershellscript)
- [Set-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/set-cmtssteprunpowershellscript)

### Properties for Run PowerShell Script

On the **Properties** tab for this step, configure the settings described in this section.

#### Package

Specify the Configuration Manager package that contains the PowerShell script. One package can contain multiple PowerShell scripts.

#### Script name

Specifies the name of the PowerShell script to run. This field is required.

#### Enter a PowerShell script

<!-- 3556028 -->
Directly enter Windows PowerShell code in this step. This feature lets you run PowerShell commands during a task sequence without first creating and distributing a package with the script.

When you add or edit a script, the PowerShell script window provides the following actions:

- Edit the script directly

- Open an existing script from file

- Browse to an existing approved [script](../../apps/deploy-use/create-deploy-scripts.md) in Configuration Manager

#### Parameters

Specifies the parameters passed to the PowerShell script. These parameters are the same as the PowerShell script parameters on the command line.

Provide parameters consumed by the script, not for the Windows PowerShell command line.

The following example contains valid parameters:

`-MyParameter1 MyValue1 -MyParameter2 MyValue2`

The following example contains invalid parameters. The first two items are Windows PowerShell command-line parameters (**-NoLogo** and **-ExecutionPolicy Unrestricted**). The script doesn't consume these parameters.

`-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`

<!-- SCCMDocs-pr issue 3561 -->
If a parameter value includes a special character or a space, use single quotation marks (`'`) around the value. Using double quotation marks (`"`) may cause the task sequence step to incorrectly process the parameter.

For example: `-Arg1 '%TSVar1%' -Arg2 '%TSVar2%'`

You can also set this property to a variable.<!-- 5690481 --> For example, if you specify `%MyScriptVariable%`, when the task sequence runs the script, it adds the value of this custom variable to the PowerShell command line.

#### PowerShell execution policy

Determine which PowerShell scripts (if any) you allow to run on the computer. Choose one of the following execution policies:

- **AllSigned**: Only run scripts signed by a trusted publisher.

- **Undefined**: Don't define any execution policy.

- **Bypass**: Load all configuration files and run all scripts. If you download an unsigned script from the internet, Windows PowerShell doesn't prompt for permission before running the script.

> [!IMPORTANT]
> PowerShell 1.0 doesn't support Undefined and Bypass execution policies.

#### Output to task sequence variable

<!-- 3556028 -->
Save the script output to a custom task sequence variable.

> [!NOTE]
> Configuration Manager limits this output to the last 1000 characters.

For an example of how to use this step property, see [How to set variables](using-task-sequence-variables.md#bkmk_run-ps).

#### Start in

<!-- 3556028 -->
Specify the starting folder for the script, up to 127 characters. This folder can be an absolute path on the destination computer or a path relative to the distribution point folder that contains the package. This field is optional.

> [!NOTE]
> The **Browse** button browses the local computer for files and folders. Anything you select must also exist on the destination computer. It must exist in the same location and with the same file and folder names.

#### Time-out

<!-- 3556028 -->
Specify a value that represents how long Configuration Manager allows the PowerShell script to run. This value can be from one minute to 999 minutes. The default value is 15 minutes. This option is disabled by default.

> [!IMPORTANT]
> If you enter a value that doesn't allow enough time for the specified script to complete successfully, this step fails. The entire task sequence could fail depending on step or group conditions. If the time-out expires, Configuration Manager terminates the PowerShell process.

#### Run this step as the following account

<!-- 3556028 -->
Specify that the PowerShell script is run as a Windows user account other than the Local System account.

> [!NOTE]
> To run simple scripts or commands with another account after installing the OS, first add the account to the computer. Additionally, you may need to restore Windows user profiles to run more complex actions.

#### Account

<!-- 3556028 -->
Specify the Windows user account this step uses to run the PowerShell script. The specified account must be a local administrator on the system and the script runs with the permissions of this account. Select **Set** to specify the local user or domain account. For more information on the task sequence run-as account, see [Accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

> [!IMPORTANT]
> If this step specifies a user account and runs in Windows PE, the action fails. You can't join Windows PE to a domain. The **smsts.log** file records this failure.

### Options for Run PowerShell Script

Besides the default options, configure the following additional settings on the **Options** tab of this task sequence step:

#### Success codes

<!-- 3556028 -->
Include other exit codes from the script that the step should evaluate as success.



## <a name="child-task-sequence"></a> Run Task Sequence

This step runs another task sequence. It creates a parent-child relationship between the task sequences. With child task sequences, you can create more modular, reusable task sequences.

To add this step in the task sequence editor, select **Add**, select **General**, and select **Run Task Sequence**.

### Specifications and limitations for Run Task Sequence

Consider the following points when you add a child task sequence to a task sequence:

- The parent and child task sequences are effectively combined into a single policy that the client runs.

- The environment is global. If the parent task sequence sets a variable, and then the child task sequence changes that variable, it retains the latest value. If the child task sequence creates a new variable, it's available for the rest of the parent task sequence.

- Status messages are sent per normal for a single task sequence operation.

- The task sequence writes entries to the **smsts.log** file, with new log entries that make it clear when a child task sequence starts.

<!--the following points are from SCCMdocs issue #1079-->

- You can't select a task sequence with a boot image reference. For any deployment that requires a boot image, specify it on the parent task sequence.

- If a child task sequence is disabled, the deployment fails. You can't use the **Continue on error** option to work around this limitation.

- If a child task sequence contains steps that are considered *high impact*, Software Center doesn't detect it and show the high-impact notification. Modify the properties of the parent task sequence, on the User Notification tab, to specify that **This is a high-impact task sequence**.

- If a child task sequence has a missing package reference, viewing the parent task sequence doesn't detect this state. If you edit the parent task sequence, it detects any missing references in child task sequences when you make changes to the parent.

### Cmdlets for Run Task Sequence

Manage this step with the following PowerShell cmdlets:<!-- 2839943, SCCMDocs#1118 -->

- [Get-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/get-cmtsstepruntasksequence)
- [New-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/new-cmtsstepruntasksequence)
- [Remove-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/remove-cmtsstepruntasksequence)
- [Set-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/set-cmtsstepruntasksequence)

### Properties for Run Task Sequence

On the **Properties** tab for this step, configure the settings described in this section.

#### Select task sequence to run

Select **Browse** to select the child task sequence. The **Select a Task Sequence** dialog box doesn't display the parent task sequence.



## <a name="BKMK_SetDynamicVariables"></a> Set Dynamic Variables

Use this step to perform the following actions:

1. Gather information from the computer and its environment. Then set specified task sequence variables with the information.

2. Evaluate defined rules. Set task sequence variables based on the rules that evaluate to true.

This step can be run in either the full OS or Windows PE.

To add this step in the task sequence editor, select **Add**, select **General**, and select **Set Dynamic Variables**.

### Variables for Set Dynamic Variables

The task sequence automatically sets the following read-only task sequence variables:

- [\_SMSTSMake](task-sequence-variables.md#SMSTSMake)
- [\_SMSTSModel](task-sequence-variables.md#SMSTSModel)
- [\_SMSTSMacAddresses](task-sequence-variables.md#SMSTSMacAddresses)
- [\_SMSTSIPAddresses](task-sequence-variables.md#SMSTSIPAddresses)
- [\_SMSTSSerialNumber](task-sequence-variables.md#SMSTSSerialNumber)
- [\_SMSTSAssetTag](task-sequence-variables.md#SMSTSAssetTag)
- [\_SMSTSUUID](task-sequence-variables.md#SMSTSUUID)

### Cmdlets for Set Dynamic Variables

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/get-cmtsstepsetdynamicvariable)
- [New-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/new-cmtsstepsetdynamicvariable)
- [Remove-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/remove-cmtsstepsetdynamicvariable)
- [Set-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/set-cmtsstepsetdynamicvariable)
- [New-CMTSRule](/powershell/module/configurationmanager/new-cmtsrule)

### Properties for Set Dynamic Variables

On the **Properties** tab for this step, configure the settings described in this section.

#### Dynamic rules and variables

To set a dynamic variable for use in the task sequence, add a rule. Then set a value for each variable specified in the rule. Additionally, add one or more variables without adding a rule. When you add a rule, choose from the following categories:

- **Computer**: Evaluate values for hardware asset tag, UUID, serial number, or MAC address. Set multiple values as necessary. If any value is true, then the rule evaluates as true. For example, the following rule evaluates as true if the device serial number is 5892087 and the MAC address is 22-A4-5A-13-78-26:

    `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`

- **Location**: Evaluate values for the default network gateway

- **Make and Model**: Evaluate values for the make and model of a computer. Both the make and model must evaluate to true for the rule to evaluate to true.

    Specify an asterisk (`*`) and question mark (`?`) as wild cards characters. The asterisk matches multiple characters and the question mark matches a single character. For example, the string `DELL*900?` matches both `DELL-ABC-9001` and `DELL9009`.

- **Task Sequence Variable**: Add a [task sequence variable](task-sequence-variables.md), condition, and value to evaluate. The conditions are the same as for [step conditions](using-task-sequence-variables.md#bkmk_access-condition). The rule evaluates to true when the value set for the variable meets the specified condition.

    Specify one or more variables to set for a rule that evaluates to true, or set variables without using a rule. Select an existing variable, or create a custom variable.

  - **Existing task sequence variables**: Select one or more variables from a list of existing task sequence variables. Array variables aren't available to select.

  - **Custom task sequence variables**: Define a custom task sequence variable. You can also specify an existing task sequence variable. This setting is useful to specify an existing variable array, such as **OSDAdapter**, since variable arrays aren't in the list of existing task sequence variables.

After you select the variables for a rule, provide a value for each variable. The variable is set to the specified value when the rule evaluates to true. For each variable, you can select **Do not display this value** to hide the value of the variable. By default, some existing variables hide values, such as the **OSDCaptureAccountPassword** variable.

> [!IMPORTANT]
> When you import a task sequence with the **Set Dynamic Variables** step, Configuration Manager removes any variable values marked as **Do not display this value**. After you import the task sequence, re-enter the value for the dynamic variable.

When you use the option **Do not display this value**, the value of the variable isn't displayed in the task sequence editor. The task sequence log file (**smsts.log**) or the task sequence debugger won't show the variable value either. The variable can still be used by the task sequence when it runs. If you no longer want these variables to be hidden, delete them first. Then redefine the variables without selecting the option to hide them.

> [!WARNING]
> If you include variables in the **Run Command Line** step's command line, the task sequence log file displays the full command line including the variable values. To prevent potentially sensitive data from appearing in the log file, set the task sequence variable **OSDDoNotLogCommand** to `TRUE`.


## <a name="BKMK_SetTaskSequenceVariable"></a> Set Task Sequence Variable

Use this step to set the value of a variable that's used with the task sequence.

This step can be run in either the full OS or Windows PE.

To add this step in the task sequence editor, select **Add**, select **General**, and select **Set Task Sequence Variable**.

### Variables for Set Task Sequence Variable

Task sequence variables are read by task sequence actions and specify the behavior of those actions. For more information about specific task sequence variables and how to use them, see the following articles:

- [How to use task sequence variables](using-task-sequence-variables.md)
- [Task sequence variables](task-sequence-variables.md)

### Cmdlets for Set Task Sequence Variable

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetVariable](/powershell/module/configurationmanager/get-cmtsstepsetvariable)
- [New-CMTSStepSetVariable](/powershell/module/configurationmanager/new-cmtsstepsetvariable)
- [Remove-CMTSStepSetVariable](/powershell/module/configurationmanager/remove-cmtsstepsetvariable)
- [Set-CMTSStepSetVariable](/powershell/module/configurationmanager/set-cmtsstepsetvariable)

### Properties for Set Task Sequence Variable

On the **Properties** tab for this step, configure the settings described in this section.

#### Task sequence variable

Specify the name of a task sequence built-in or action variable, or specify your own user-defined variable name.

#### Do not display this value

<!--1358330-->
Enable this option to mask sensitive data stored in task sequence variables. For example, when specifying a password.

> [!NOTE]
> Enable this option and then set the value of the task sequence variable. Otherwise the variable value isn't set as you intend, which may cause unexpected behaviors when the task sequence runs.<!--SCCMdocs issue #800-->

When you use the option **Do not display this value**, the value of the variable isn't displayed in the task sequence editor. The task sequence log file (**smsts.log**) or the task sequence debugger won't show the variable value either. The variable can still be used by the task sequence when it runs. If you no longer want this variable to be hidden, delete it first. Then redefine the variable without selecting the option to hide it.

> [!WARNING]
> If you include variables in the **Run Command Line** step's command line, the task sequence log file displays the full command line including the variable values. To prevent potentially sensitive data from appearing in the log file, set the task sequence variable **OSDDoNotLogCommand** to `TRUE`.<!-- 6963278 -->

#### Value

The task sequence sets the variable to this value. Set this task sequence variable to the value of another task sequence variable with the syntax `%varname%`.



## <a name="BKMK_SetupWindowsandConfigMgr"></a> Setup Windows and ConfigMgr

Use this step to perform the transition from Windows PE to the new OS. This task sequence step is a required part of any OS deployment. It installs the Configuration Manager client into the new OS, and prepares for the task sequence to continue execution in the new OS.

This step is responsible for transitioning the task sequence from Windows PE to the full OS. The step runs both in Windows PE and the full OS because of this transition. However, since the transition starts in Windows PE, it can only be added during the Windows PE portion of the task sequence.

This step replaces sysprep.inf or unattend.xml directory variables, such as `%WINDIR%` and `%ProgramFiles%`, with the Windows PE installation directory, `X:\Windows`. The task sequence ignores variables specified by using these environment variables.

To add this step in the task sequence editor, select **Add**, select **Images**, and select **Setup Windows and ConfigMgr**.

### Behaviors for Setup Windows and ConfigMgr

This step performs the following actions:

#### Preliminaries: Windows PE

1. Substitute task sequence variables in the unattend.xml file.

2. Download the package that contains the Configuration Manager client. Add the package to the deployed image.

#### Set up Windows

- Image-based installation

    1. Disable the Configuration Manager client in the image, if it exists. In other words, disable Autostart for the Configuration Manager client service.

    2. Update the registry in the deployed image to start the deployed OS with the same drive letter as the reference computer.

    3. Restart to the deployed OS.

    4. Windows mini-setup runs by using the previously specified sysprep.inf or unattend.xml answer file that has all end-user interaction suppressed. If you use the **Apply Network Settings** step to join a domain, then that information is in the answer file. Windows mini-setup joins the computer to the domain.

- Setup.exe-based installation. Runs Setup.exe that follows the typical Windows setup process:

    1. Copy the OS upgrade package, specified in the **Apply Operating System** step, to the hard disk drive.

    2. Restart to the newly deployed OS.

    3. Windows mini-setup runs by using the previously specified sysprep.inf or unattend.xml answer file that has all user interface settings suppressed. If you use the  **Apply Network Settings** step to join a domain, then that information is in the answer file. Windows mini-setup joins the computer to the domain.

#### Set up the Configuration Manager client

1. After Windows mini-setup finishes, the task sequence resumes by using setupcomplete.cmd. For more information, see [Run a script after setup is complete (SetupComplete.cmd)](/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd).

2. Enable or disable the local Administrator account, based on the option selected in the **Apply Windows Settings** step.

3. Install the Configuration Manager client by using the previously downloaded package, and installation properties specified in this step. The client installs in "provisioning mode". This mode prevents the client from processing new policy requests until the task sequence completes. For more information, see [Provisioning mode](provisioning-mode.md).

4. Wait for the client to be fully operational.

#### The step completes

The task sequence continues running the next step.

> [!NOTE]
>
> The task sequence transitions from Windows PE to the newly installed Windows OS during the **Setup Windows and ConfigMgr** task. When the newly installed Windows starts for the first time, Windows Setup runs. At the end of Windows Setup, the task sequence is relaunched by the Windows Setup script **SetupComplete.cmd**. This results in the task sequence running entirely within Windows Setup. Windows group policy normally doesn't process until after Windows Setup is complete, so therefore group policy isn't processed until the task sequence is complete. This behavior is consistent across different versions of Windows. For more information on the order of operations, see [Run a script after setup is complete (SetupComplete.cmd)](/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd).<!-- 2841304 -->
>
> Although group policy doesn't normally run until Windows Setup and the task sequence completes, Windows and the task sequence engine don't block group policy from running. Some actions such as scripts, application installs, or certain task sequence steps run during the task sequence can trigger group policy evaluation. For example, the [Install Software Updates](#BKMK_InstallSoftwareUpdates) task may trigger group policy evaluation when it sets WSUS server. A script that calls gpupdate could also trigger a group policy refresh.

### Variables for Setup Windows and ConfigMgr

Use the following task sequence variables with this step:

- [SMSClientInstallProperties](task-sequence-variables.md#SMSClientInstallProperties)

### Cmdlets for Setup Windows and ConfigMgr

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/get-cmtsstepsetupwindowsandconfigmgr)
- [New-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/new-cmtsstepsetupwindowsandconfigmgr)
- [Remove-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/remove-cmtsstepsetupwindowsandconfigmgr)
- [Set-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/set-cmtsstepsetupwindowsandconfigmgr)

### Properties for Setup Windows and ConfigMgr

On the **Properties** tab for this step, configure the settings described in this section.

#### Client package

Select **Browse**, then choose the Configuration Manager client installation package to use with this step.

#### Use pre-production client package when available

If there's a pre-production client package available, and the computer is a member of the piloting collection, the task sequence uses this package instead of the production client package. The pre-production client is a newer version for testing in the production environment. Select **Browse**, then choose the pre-production client installation package to use with this step.

#### Installation Properties

The task sequence step automatically specifies site assignment and the default configuration. Use this field to specify any additional installation properties to use when you install the client. To enter multiple installation properties, separate them with a space.

Specify command-line options to use during client installation. For example, enter `/skipprereq: silverlight.exe` to inform CCMSetup.exe to not install the Microsoft Silverlight prerequisite. For more information about available command-line options for CCMSetup.exe, see [About client installation properties](../../core/clients/deploy/about-client-installation-properties.md).

When you run an OS deployment task sequence on an internet-based client, that's either Microsoft Entra joined or uses token-based authentication, you need to specify the [CCMHOSTNAME](../../core/clients/deploy/about-client-installation-properties.md#ccmhostname) property in the **Setup Windows and ConfigMgr** step. For example, `CCMHOSTNAME=OTTERFALLS.CLOUDAPP.NET/CCM_Proxy_MutualAuth/12345678907927939`.

### Options for Setup Windows and ConfigMgr

> [!NOTE]
> Don't enable **Continue on error** on the **Options** tab. If there's an error during this step, the task sequence fails whether or not you enable this setting.



## <a name="BKMK_UpgradeOS"></a> Upgrade Operating System

Use this step to upgrade an earlier version of Windows to a later version of Windows.

This task sequence step runs only in the full OS. It doesn't run in Windows PE.

To add this step in the task sequence editor, select **Add**, select **Images**, and select **Upgrade Operating System**.

> [!TIP]
> Windows 11 and Windows 10 media include multiple editions. When you configure a task sequence to use an OS upgrade package or OS image, be sure to select a [supported edition](../../core/plan-design/configs/support-for-windows-11.md#support-notes).
>
> Use content pre-caching to download an applicable OS upgrade package before a user installs the task sequence. For more information, see [Configure pre-cache content](../deploy-use/configure-precache-content.md).

### Variables for Upgrade OS

Use the following task sequence variables with this step:

- [_SMSTSOSUpgradeActionReturnCode](task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)
- [SetupCompletePause](task-sequence-variables.md#SetupCompletePause)
- [OSDSetupAdditionalUpgradeOptions](task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)

### Cmdlets for Upgrade OS

Manage this step with the following PowerShell cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepUpgradeOperatingSystem)
- [New-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/New-CMTSStepUpgradeOperatingSystem)
- [Remove-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Remove-CMTSStepUpgradeOperatingSystem)
- [Set-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Set-CMTSStepUpgradeOperatingSystem)

### Properties for Upgrade OS

On the **Properties** tab for this step, configure the settings described in this section.

#### Upgrade package

Select this option to specify the Windows OS upgrade package to use for the upgrade.

#### Source path

Specifies a local or network path to the Windows media that Windows Setup uses. This setting corresponds to the Windows Setup command-line option `/InstallFrom`.

You can also specify a variable, such as `%MyContentPath%` or `%DPC01%`. When you use a variable for the source path, set its value earlier in the task sequence. For example, use the [Download Package Content](#BKMK_DownloadPackageContent) step to specify a variable for the location of the OS upgrade package. Then, use that variable for the source path for this step.

#### Edition

Specify the edition within the OS media to use for the upgrade.

#### Product key

Specify the product key to apply to the upgrade process.

#### Install the following feature updates

<!--3555906-->
Starting in version 2103, select this option to upgrade a client's Windows OS by using a feature update. This option uses content that you synchronize through the software update point. The size of the servicing ESD file is generally smaller than the OS upgrade package and WIM image file.

Select the new button (gold asterisk), and add a feature update.

> [!NOTE]
> You can only add feature updates.

If your environment supports multiple languages or architectures, add multiple feature updates to the step. The client uses the first applicable update that's not superseded by any other deployed updates.

The user experience with a feature update in a task sequence is the same as with an OS upgrade package.

#### Provide the following driver content to Windows Setup during upgrade

Add drivers to the destination computer during the upgrade process. The drivers must be compatible with Windows 10 or later. This setting corresponds to the Windows Setup command-line option `/InstallDriver`. For more information, see [Windows Setup command-line options](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#installdrivers).

Specify one of the following options:

- **Driver package**: Select **Browse** and choose an existing driver package from the list.

- **Staged content**: Select this option to specify the location for the driver content. You can specify a local folder, network path, or a task sequence variable. When you use a variable for the source path, set its value earlier in the task sequence. For example, by using the [Download Package Content](task-sequence-steps.md#BKMK_DownloadPackageContent) step.

> [!TIP]
> If you want to have dynamic content for multiple types of hardware:
>
> - Use multiple instances of this step with conditions for the hardware types and separate driver content.
>
> - Use multiple instances of the [Download Package Content](task-sequence-steps.md#BKMK_DownloadPackageContent) step. Place the content in a common location, and then use the **Staged content** option. The benefit of this method is the task sequence has a single **Upgrade OS** step.

> [!NOTE]
> This option is not compatible with feature updates.

#### Time-out (minutes)

Specify the number of minutes before Configuration Manager fails this step. This option is useful if Windows Setup stops processing but doesn't terminate.

#### Perform Windows Setup compatibility scan without starting upgrade

Perform the Windows Setup compatibility scan without starting the upgrade process. This setting corresponds to the Windows Setup command-line option `/Compat ScanOnly`. Deploy the entire OS upgrade package with this option.

<!--SCCMDocs-pr issue 2812-->
When you enable this option, this step doesn't put the Configuration Manager client into provisioning mode. Windows Setup runs silently in the background, and the client continues to function as normal. For more information, see [Provisioning mode](provisioning-mode.md).

Setup returns an exit code as a result of the scan. The following table provides some of the more common exit codes:

|Exit code|Details|
|-|-|
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|No compatibility issues ("success").|
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Actionable compatibility issues.|
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|Selected migration choice isn't available. For example, an upgrade from Enterprise to Professional.|
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Not eligible for Windows 10.|
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Not enough free disk space.|

For more information about this parameter, see [Windows Setup Command-Line Options](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#compat).

#### Ignore any dismissible compatibility messages

Specifies that Setup completes the installation, ignoring any dismissible compatibility messages. This setting corresponds to the Windows Setup command-line option `/Compat IgnoreWarning`.

#### Dynamically update Windows Setup with Windows Update

Enable setup to perform Dynamic Update operations, such as search, download, and install updates. This setting corresponds to the Windows Setup command-line option `/DynamicUpdate`. This setting isn't compatible with Configuration Manager software updates. Enable this option when you manage updates with stand-alone Windows Server Update Services (WSUS) or Windows Update client policies.

#### Override policy and use default Microsoft Update

Temporarily override the local policy in real time to run Dynamic Update operations. The computer gets updates from Windows Update.
