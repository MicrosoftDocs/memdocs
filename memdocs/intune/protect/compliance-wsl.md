---
# required metadata

title: Compliance for Windows Subsystem for Linux  
description: Evaluate WSL attributes on a host device for compliance. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby 
ms.date: 11/19/2024 
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
ms.reviewer: ilwu
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- compliance
- sub-device-compliance
---

# Evaluate compliance for Windows Subsystem for Linux   

**Applies to**: 
- Windows 10   
- Windows 11   

Create a Microsoft Intune policy that checks the compliance of devices running Windows Subsystem for Linux (WSL). Microsoft Intune incorporates the WSL compliance results into the overall compliance state of the host device so that you can see the whole health of the device.

This article describes how to set up compliance checks for WSL.  

## Requirements   

To create your compliance policy with WSL settings, you must meet these requirements:  

- The [Intune WSL plugin](https://go.microsoft.com/fwlink/?linkid=2296896) must be installed for compliance evaluation.  
  
- The Microsoft Intune management extension must be installed on the target device. Make sure devices meet one of the following conditions so that the management extension can install:
  
   - Assign a PowerShell script or a proactive remediation to the user or device.  
   - Deploy a Win32 app or Microsoft Store app to the user or device.
   - Assign a custom compliance policy to the user or device.

## Before you begin

Unassign and remove existing custom compliance policies for WSL. Then review the [limitations](#limitations) with WSL settings in compliance policies so that you know what to expect.  

## Add Intune WSL plugin as a Win32 app

Create a Win32 app policy for the [Intune WSL plugin](https://github.com/microsoft/shell-intune-samples/blame/master/Linux/WSL/IntuneWSLPluginInstaller/IntuneWSLPluginInstaller.msi), and assign it to the target Microsoft Entra group.  

1. Use the [Microsoft Win32 Content Prep Tool](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool) to convert the Intune WSL plugin to the *.intunewin* format. For more information, see [Convert the Win32 app content](../apps/apps-win32-prepare.md#convert-the-win32-app-content).

2. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as at least an Intune administrator.

3. Go to **Apps** > **All apps** > **Add**.  

4. For **App type**, scroll down to **Other**, and then select **Windows app (Win32)**.  

5. Choose **Select**. The **Add app** steps appear.  

6. Choose **Select app package file**.

7. Select the **Folder** button and browse your files for the app package file. Upload the Intune WSL plugin installation file with the *.intunewin* extension.  

8. Select **OK** to continue.  

9. Enter the following app information:  
   - **Select file**: The app package file you selected in the previous step appears here. Select the file to upload a different installation package file for the Intune WSL plugin.   
   - **Name**: Enter **Intune WSL Plugin**.  
   - **Description**: Select **Edit Description** to enter a description for the app. For example, you can describe its purpose or how your organization plans to use it. This setting is optional but recommended.  
   - **Publisher**: Enter **Microsoft Intune**.  

10. Select **Next** to go to **Program**.  

11. Review the settings that are prepopulated so that you're familiar with how the app behaves. Leave the settings as-is.  

12. Select **Next** to go to **Requirements**.  

13. Enter the requirements devices must meet to install the app.  

14. Select **Next** to go to **Detection rules**.

15. Review the detection rules that are prepopulated. These rules are app-specific and detect the presence of the app. Leave the settings as-is.    

16. Select **Next** to go to **Dependencies**. Leave the settings as-is.

17. Select **Next** to go to **Supersedence**. Leave the settings as-is.

18. Select **Next** to go to **Assignments**.  

19. To assign the policy, add Microsoft Entra users under **Required**.   

20. Select **Next** to go to **Review + create**.  

21. Review the summary, and then select **Create** to save the policy.  

> [!NOTE]
> When you create a compliance policy with WSL settings, it automatically generates a read-only custom script. Editing the compliance policy also edits the associated custom script. These scripts appear in the Microsoft Intune admin center in **Devices** > **Compliance** > **Scripts** and are called *Built-in WSL Compliance-< compliance policy id >*.  

## Limitations

This section describes the known limitations with using the Intune WSL plugin for compliance evaluation. 

- Compliance evaluation requires the installed Linux distributions in WSL to run at least one time before it works. If you install a Linux distribution with the `--no-launch` [command for WSL](/windows/wsl/basic-commands), the compliance evaluation won't work.   

- Compliance evaluation might not function as expected on custom Linux images or Linux images without the `etc/os-release` directory. 

- Even with the Intune WSL plugin, it's possible for malicious software or user actions to compromise the compliance evaluation mechanism. 

## Next steps

- [Create a compliance policy](create-compliance-policy.md#create-the-policy), and set the **Platform** to **Windows 10 and later**. For more information about the compliance settings for Windows Subsystem for Linux, see [Windows Subsystem for Linux](compliance-policy-create-windows.md#windows-subsystem-for-linux).   

- [Add actions for noncompliant devices](actions-for-noncompliance.md) and [use scope tags to filter policies](../fundamentals/scope-tags.md).  

- [Monitor your compliance policies](compliance-policy-monitor.md).  

- For troubleshooting help, see [Troubleshooting Windows Subsystem for Linux](/windows/wsl/troubleshooting).   
