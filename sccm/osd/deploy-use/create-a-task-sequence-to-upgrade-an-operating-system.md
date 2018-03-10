---
title: Create a task sequence to upgrade an operating system
titleSuffix: Configuration Manager
description: Use a task sequence to automatically upgrade from Windows 7 or later to Windows 10
ms.custom: na
ms.date: 03/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Create a task sequence to upgrade an operating system in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use task sequences in Configuration Manager to automatically upgrade an operating system on a destination computer. This upgrade can be from Windows 7 or later to Windows 10, or from Windows Server 2012 or later to Windows Server 2016. Create a task sequence that references the OS upgrade package and any other content to install, such as applications or software updates. The task sequence to upgrade an operating system is part of the [Upgrade Windows to the latest version](upgrade-windows-to-the-latest-version.md) scenario.  



##  <a name="BKMK_UpgradeOS"></a> Create a task sequence to upgrade an operating system  
 To upgrade the operating system on computers, you can create a task sequence and select **Upgrade an operating system from upgrade package** in the Create Task Sequence Wizard. The wizard adds the task sequence steps to upgrade the operating system, apply software updates, and install applications. Before you create the task sequence, the following requirements must be in place:    

-   **Required**  

     - The [operating system upgrade package](../get-started/manage-operating-system-upgrade-packages.md) must be available in the Configuration Manager console.
     - When upgrading to Windows Server 2016, select the **Ignore any dismissable compatibility messages** setting in the Upgrade Operating System task sequence step. Otherwise the upgrade fails.

-   **Required (if used)**  

    -   [Software updates](../../sum/get-started/synchronize-software-updates.md) must be synchronized in the Configuration Manager console.  

    -   [Applications](../../apps/deploy-use/create-applications.md) must be added to the Configuration Manager console.  

#### To create a task sequence that upgrades an operating system  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  On the **Home** tab, in the **Create** group, click **Create Task Sequence** to start the Create Task Sequence Wizard.  

4.  On the **Create a New Task Sequence** page, click **Upgrade an operating system from upgrade package**, and then click **Next**.  

5.  On the **Task Sequence Information** page, specify the following settings, and then click **Next**.  

    -   **Task sequence name**: Specify a name that identifies the task sequence.  

    -   **Description**: Specify a description of the task that is performed by the task sequence.  

6.  On the **Upgrade the  Windows Operating System** page, specify the following settings, and then click **Next**.  

    -   **Upgrade package**: Specify the upgrade package that contains the operating system upgrade source files. You can verify  that you have selected the correct upgrade package by looking at the information in the **Properties** pane. For more information, see [Manage operating system upgrade packages](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Edition index**: If there are multiple operating system edition indexes available in the package, select the desired edition index. By default, the first item is selected.  

    -   **Product key**: Specify the product key for the Windows operating system to install. You can specify encoded volume license keys and standard product keys. If you use a non-encoded product key, each group of five characters must be separated by a dash (-). For example: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. When the upgrade is for a volume license edition, the product key is not required. You only need a product key when the upgrade is for a retail Windows edition.  

    -   **Ignore any dismissable compatibility messages**: Select this setting if you are upgrading to Windows Server 2016. If you do not select this setting, the task sequence fails to complete because Windows Setup is waiting for the user to click **Confirm** on a Windows app compatibility dialog.   

7.  On the **Include Updates** page, specify whether to install required, all, or no software updates. Then click **Next**. If you specify to install software updates, Configuration Manager installs only those software updates targeted to the collections of which the destination computer is a member.  

8.  On the **Install Applications** page, specify the applications to install on the destination computer, and then click **Next**. If you specify multiple applications, you can also specify that the task sequence continues if the installation of a specific application fails.  

9. Complete the wizard.  


 > [!Important] 
 > When the task sequence is complete, the client does not remove the post-processing and rollback scripts until the computer is restarted. These script files do not contain sensitive information.  


 > [!Note]
 > Starting in version 1802, the default task sequence template for Windows 10 in-place upgrade includes additional groups with recommended actions to add before and after the upgrade process. These actions are common among many customers who are successfully upgrading devices to Windows 10. For more information, see recommended task sequence steps [to prepare for upgrade](#recommended-task-sequence-steps-to-prepare-for-upgrade) and [for post-processing](#recommended-task-sequence-steps-for-post-processing).



## Configure pre-cache content
The pre-cache feature for available deployments of task sequences lets clients download relevant OS upgrade package content before a user installs the task sequence.
> [!TIP]  
> This feature was first introduced in version 1702 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1706, this feature is no longer a pre-release feature.

For example, you only want a single in-place upgrade task sequence for all users, and have many architectures and languages. In previous versions, the content starts to download when the user installs an available task sequence deployment from Software Center. This delay adds additional time before the installation is ready to start. All content referenced in the task sequence is downloaded. This content includes the operating system upgrade package for all languages and architectures. If each upgrade package is roughly three GB in size, the total content is very large.

Pre-cache content gives you the option to allow the client to only download the applicable OS upgrade package, as well as all other referenced content, as soon as it receives the deployment. When the user clicks **Install** in Software Center, the content is ready and the installation starts quickly because the content is on the local hard drive.

 > [!NOTE]
 > This behavior currently only applies to the OS upgrade package. That package is the only content on which you specify the matching architecture or language. For example, if the task sequence also references multiple driver packages, the client currently downloads them all. The task sequence engine evaluates the conditions on the steps when the task sequence runs, not in advance. The client uses the tags on the package properties to determine which content to pre-cache.

### To configure the pre-cache feature

1. Create OS upgrade packages for specific architectures and languages. Specify the architecture and language on the **Data Source** tab of the package. For the language, use the decimal conversion. For example, 1033 is the decimal value for English, and 0x0409 is the hexadecimal equivalent.

    The client evaluates the architecture and language values to determine which OS upgrade package it downloads during pre-caching.

1. Create a task sequence with conditional steps for the different languages and architectures. For example, the following step uses the English version:

    ![Task sequence editor showing multiple Upgrade OS steps for ENU, DEU, and JPN](../media/precacheproperties2.png)

    ![Task sequence editor, Options tab, displaying the WMI WQL query for Locale and OSArchitecture](../media/precacheoptions2.png)  

3. Deploy the task sequence. For the pre-cache feature, configure the following settings:
    - On the **General** tab, select **Pre-download content for this task sequence**.
    - On the **Deployment settings** tab, configure the task sequence with the **Available** for **Purpose**.
    - On the **Scheduling** tab, for the **Schedule when this deployment will be available** setting, choose the currently selected time. The client starts pre-caching content at the deployment's available time. When a targeted client receives this policy, the available time is in the past, thus pre-cache download starts right away. If the client receives this policy but the available time is in the future, the client does not start pre-caching content until the available time occurs. 
    - On the **Distribution Points** tab, configure the **Deployment options** settings. If the content is not pre-cached before a user starts the installation, the client uses these settings.
  

### User experience
- When the client receives the deployment policy, it starts to pre-cache the content after the deployment's available time. This content includes all referenced packages, but only the OS upgrade package that matches the architecture and language attributes on the package.
- When the client makes the deployment available to users, a notification displays to inform users about the new deployment. Now the task sequence is visible in Software Center. The user can go to Software Center and click **Install** to start the installation.
- If the content is not fully pre-cached when the user installs the task sequence, then the client uses the settings that you specify on the **Deployment Option** tab of the deployment. 



## Recommended task sequence steps to prepare for upgrade

Starting in version 1802, the default task sequence template for Windows 10 in-place upgrade includes additional groups with recommended actions to add before the upgrade process. These actions in the **Prepare for Upgrade** group are common among many customers who are successfully upgrading devices to Windows 10. For sites on versions prior to 1802, manually add these actions to your task sequence in the **Prepare for Upgrade** group.
- **Battery checks**: Add steps in this group to check whether the computer is using battery, or wired power. This action requires a custom script or utility to perform this check.
- **Network/wired connection checks**: Add steps in this group to check whether the computer is connected to a network, and is not using a wireless connection. This action requires a custom script or utility to perform this check.
- **Remove incompatible applications**: Add steps in this group to remove any applications that are incompatible with this version of Windows 10. The method to uninstall an application varies. If the application uses Windows Installer, copy the **Uninstall program** command line from the **Programs** tab on the Windows Installer deployment type properties of the application. Then add a **Run Command Line** step in this group with the uninstall program command line. For example: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Remove incompatible drivers**: Add steps in this group to remove any drivers that are incompatible with this version of Windows 10.
- **Remove/suspend third-party security**: Add steps in this group to remove or suspend third-party security programs, such as antivirus.
   - If you are using a third-party disk encryption program, provide its encryption driver to Windows Setup with the **/ReflectDrivers** [command-line option](/windows-hardware/manufacture/desktop/windows-setup-command-line-options). Add a [Set Task Sequence Variable](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) step to the task sequence in this group. Set the task sequence variable to **OSDSetupAdditionalUpgradeOptions**. Set the value to **/ReflectDriver** with the path to the driver. This [task sequence action variable](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system) appends the Windows Setup command-line used by the task sequence. Contact your software vendor for any additional guidance on this process.

### Download Package Content task sequence step  
 The [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) step can be used before the **Upgrade Operating System** step in the following scenarios:  

-   You use a single upgrade task sequence for both x86 and x64 platforms. Include two **Download Package Content** steps in the **Prepare for Upgrade** group. Set conditions on each step to detect the client architecture. This condition causes the step to download only the appropriate operating system upgrade package. Configure each **Download Package Content** step to use the same variable, and use the variable for the media path on the **Upgrade Operating System** step.  

-   To dynamically download an applicable driver package, use two **Download Package Content** steps with conditions to detect the appropriate hardware type for each driver package. Configure each **Download Package Content** step to use the same variable. Then use that variable for the **Staged content** value in the drivers section on the **Upgrade Operating System** step.  

   > [!NOTE]
   > When there is more than one package, Configuration Manager adds a numerical suffix to the variable name. For example, if you specify a variable of %mycontent% as a custom variable, this location is where the client stores all referenced content. When you refer to the variable in a subsequent step, such as **Upgrade Operating System**, use the variable with a numerical suffix. In this example, %mycontent01% or %mycontent02%, where the number corresponds to the order in which the **Download Package Content** step lists this specific content.



## Recommended task sequence steps for post-processing   
 After you create the task sequence, add additional steps in the **Post-Processing** group of the task sequence.  

> [!NOTE]  
>  This task sequence is not linear. There are conditions on steps that can affect the results of the task sequence. This behavior depends on whether it successfully upgrades the client computer, or if it has to roll back the client computer to the original OS.  

Starting in version 1802, the default task sequence template for Windows 10 in-place upgrade includes additional groups with recommended actions to add after the upgrade process. These actions in the **Post-Processing** group are common among many customers who are successfully upgrading devices to Windows 10. For sites on versions prior to 1802, manually add these actions to your task sequence in the **Post-Processing** group.
- **Apply setup-based drivers**: Add steps in this group to install setup-based drivers (.exe) from packages.
- **Install/enable third-party security**: Add steps in this group to install or enable third-party security programs, such as antivirus. 
- **Set Windows default apps and associations**: Add steps in this group to set Windows default apps and file associations. First prepare a reference computer with your desired app associations. Then run the following command line to export: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Add the XML file to a package. Then add a [Run Command Line](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) step in this group. Specify the package that contains the XML file, and then specify the following command line: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> For more information, see [Export or import default application associations](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).
- **Apply customizations and personalization**: Add steps in this group to apply Start menu customizations, such as organizing program groups. For more information, see [Customize the Start screen](/windows-hardware/manufacture/desktop/customize-the-start-screen).



## Optional task sequence steps for rollback  
 When something goes wrong with the upgrade process after the computer restarts, Windows Setup will roll back the upgrade to the previous operating system. The task sequence then continues with any steps in the **Rollback** group. After you create the task sequence, you can add optional steps in the Rollback group. For example, reverse any changes made to the system in the Prepare for Upgrade group, such as uninstalling incompatible software.



## Additional recommendations
- Review Windows documentation to [Resolve Windows 10 upgrade errors](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). This article also includes detailed information about the upgrade process.
- On the default **Check Readiness** step, enable **Ensure minimum free disk space (MB)**. Set the value to at least **16384** (16 GB) for a 32-bit OS upgrade package, or **20480** (20 GB) for 64-bit. 
- Use the **SMSTSDownloadRetryCount** [built-in task sequence variable](/sccm/osd/understand/task-sequence-built-in-variables) to retry downloading policy. Currently by default, the client retries twice; this variable is set to two (2). If your clients are not on a wired corporate network connection, additional retries help the client obtain policy. Using this variable causes no negative side effect, other than delayed failure if it cannot download policy.<!-- 501016 --> Also increase the **SMSTSDownloadRetryDelay** variable from the default 15 seconds.
- Perform an inline compatibility assessment. 
   - Add a second **Upgrade Operating System** step early in the **Prepare for Upgrade** group. Name it *Upgrade assessment*. Specify the same upgrade package, and then enable the option to **Perform Windows Setup compatibility scan without starting upgrade**. Enable **Continue on error** on the Options tab. 
   - Immediately following this *Upgrade assessment* step, add a **Run Command Line** step. Specify the following command line:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>On the **Options** tab, add the following condition: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>This return code is the decimal equivalent of MOSETUP_E_COMPAT_SCANONLY (0xC1900210), which is a successful compatibility scan with no issues. If the *Upgrade Assessment* step succeeds and returns this code, this step is skipped. Otherwise, if the assessment step returns any other return code, this step fails the task sequence with the return code from the Windows Setup compatibility scan.
   - For more information, see [Upgrade operating system](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).
- If you want to change the device from BIOS to UEFI during this task sequence, see [Convert from BIOS to UEFI during an in-place upgrade](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).
