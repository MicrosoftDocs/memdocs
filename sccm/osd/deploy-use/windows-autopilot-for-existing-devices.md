---
title: Windows Autopilot for existing devices
titleSuffix: Configuration Manager
description: Use a Configuration Manager task sequence to reimage and provision a Windows 7 device for Windows Autopilot user-driven mode
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual


ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Windows Autopilot for existing devices
<!--3607717, fka 1358333-->

*Applies to: Configuration Manager (current branch)*

[Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) provides a way for organizations to ship fresh, untouched Windows 10 devices directly to the end user and define the provisioning flow the user goes through to get a secure, productive Windows 10 device. The device is registered with the Windows Autopilot service, so you can assign the necessary Windows Autopilot profile. This profile defines the out-of-box experience (OOBE) for that device. 

[Windows Autopilot for existing devices](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) is available with Windows 10, version 1809 or later. This feature allows you to reimage and provision a Windows 7 device for [Windows Autopilot user-driven mode](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) using a single, native Configuration Manager task sequence. 



## Prerequisites

- Acquire the installation media for Windows 10 version 1809, or later. Then create a Configuration Manager OS image. For more information, see [Manage OS images](/sccm/osd/get-started/manage-operating-system-images).

- In Microsoft Intune, create profiles for Windows Autopilot. For more information, see [Enroll Windows devices in Intune by using Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

- A device not already registered with the Windows Autopilot service. If the device is already registered, the assigned profile takes precedence. The Autopilot for existing devices profile only applies if that the online profile times out.



## Create the configuration file

1. On a Windows device with internet connectivity, open an administrative PowerShell command window, and run the following commands:  

    1. Install required modules, and accept prompts to continue  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. Sign in to Intune with administrator credentials  
        ``` PowerShell  
        Connect-AutopilotIntune 
        ```

    3. Retrieve all Windows Autopilot profiles associated with your Intune tenant  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. Create a configuration file for each profile. The files are named for the display name of the profile, and saved on the current user's desktop.<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > The configuration file can only contain one profile. Each profile should be inside curly brackets `{}`.  

2. Save one of the profiles to an ANSI-encoded file named **AutopilotConfigurationFile.json**. Save it to a location suitable as a Configuration Manager package source.  

    > [!Tip]  
    > If you use the PowerShell cmdlet **Out-File** to redirect the JSON output to a file, it uses Unicode encoding by default. This cmdlet may also truncate long lines. Use the **Set-Content** cmdlet with the `-Encoding ASCII` parameter to set the proper text encoding.   
    > 
    > Windows Notepad uses ANSI encoding by default.  

3. Create a Configuration Manager package that contains this file. It doesn't require a program. For more information, see [Create a package](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program).  

    > [!NOTE]  
    > Windows requires that this file is named **AutopilotConfigurationFile.json**. To use more than one Autopilot profile, create separate Configuration Manager packages.  



## Create the task sequence

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and select the **Task Sequences** node. Select **Create Task Sequence** in the ribbon.  

2. On the **Create new task sequence** page, select the option to **Deploy Windows Autopilot for existing devices**.  

3. On the **Task sequence information** page, specify a name, optionally add a description, and select a boot image. For more information on supported boot image versions, see [Support for Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

4. On the **Install Windows** page, select the Windows 10 **Image package**. Then configure the following settings:  

    - **Image index**: Select either Enterprise, Education, or Professional, as required by your organization  

    - Enable the option to **Partition and format the target computer before installing the operating system**  

    - **Configure task sequence for use with Bitlocker**: If you enable this option, the task sequence includes the steps necessary to enable Bitlocker  

    - **Product key**: If you need to specify a product key for Windows activation, enter it here  

    - Select one of the following options to configure the local administrator account in Windows 10:  
        - **Randomly generate the local administrator password and disable the account on all support platforms (recommended)**
        - **Enable the account and specify the local administrator password**

5. On the **Configure Network** page, select the option to **Join a workgroup**. This task sequence uses the Windows system preparation tool (sysprep). If the device is joined to a domain, sysprep fails.  

6. On the **Install Configuration manager** page, add any necessary installation properties for your environment.  

    > [!Tip]  
    > The task sequence only needs this information if the Configuration Manager client components are needed during the task sequence before sysprep runs. For example, to install software updates or applications. If you're not doing these actions, the client isn't needed. It's uninstalled before the task sequence runs sysprep.  

7. The **Include updates** page selects by default the option to **Do not install any software updates**.  

    > [!Tip]  
    > Use offline image servicing to keep the image up to date with the latest Windows 10 quality updates. For more information, see [Apply software updates to an OS image](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).  

8. On the **Install applications** page, you can select applications to install during the task sequence. However, Microsoft recommends that you mirror the signature image approach with this scenario. After the device provisions with Autopilot, apply all applications and configurations from Microsoft Intune or Configuration Manager co-management. This process provides a consistent experience between users receiving new devices and those using Windows Autopilot for existing devices.  

8. On the **System Preparation** page, select the package that includes the Autopilot configuration file. By default, the task sequence restarts the computer after it runs Windows Sysprep. You can also select the option to **Shutdown computer after this task sequence completes**. This option lets you prepare a device and then deliver it to a user for a consistent Autopilot experience.  

9. Complete the wizard.  

If you edit the task sequence, it's similar to the default task sequence to apply an existing OS image. This task sequence includes the following additional steps:  

- **Apply Windows Autopilot configuration**: This step applies the Autopilot configuration file from the specified package. It's not a new type of step, it's a **Run Command Line** step to copy the file.  

- **Prepare Windows for Capture**: This step runs Windows Sysprep, and has the setting to **Shutdown the computer after running this action**. For more information, see [Prepare Windows for Capture](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareWindowsforCapture).  

The Windows Autopilot for existing devices task sequence results in a device joined to Azure Active Directory (Azure AD). 

 > [!NOTE]  
 > Windows 10 1903 and 1909 Autopilot has a known issue where the **AutopilotConfigurationFile.json** file gets deleted during Sysprep. For this reason if deploying Windows 10 1903 or 1909, edit the Task Sequence created in the above steps and make the following two changes
 >1. Disable the **Prepare Windows for Capture** step
 >2. Immediately after the disalbed **Prepare Windows for Capture** step, add a new **Run Command Line** step that runs the command **c:\windows\system32\sysprep\sysprep.exe /oobe /reboot**
 > See the [Windows Autopilot - known issues](https://docs.microsoft.com/en-us/windows/deployment/windows-autopilot/known-issues) for additional information

Use OneDrive for Business [known folder move](https://docs.microsoft.com/onedrive/redirect-known-folders) to make sure the user's data is backed up before the Windows 10 upgrade.



## Next steps

Use co-management to enhance the management features of your Windows 10 devices. The second path to co-management is through modern provisioning with Windows Autopilot. For more information, see the following articles:

- [What is co-management?](/sccm/comanage/overview)
- [Paths to co-management](/sccm/comanage/quickstart-paths)
- [Windows Autopilot with co-management](/sccm/comanage/quickstart-autopilot)

## See also

- [Enroll Windows devices in Intune by using the Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)
