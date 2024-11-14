---
# required metadata

title: Compliance for Windows Subsystem for Linux  
description: Evaluate WSL attributes on a host device for compliance. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/14/2024 
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

These requirements must be followed to create your compliance policy with WSL settings:

- [Intune WSL plug-in](https://go.microsoft.com/fwlink/?linkid=2296896) must be installed for compliance evaluation.
- The Microsoft Intune management extension (IME) must be installed on the target device. This is automatically installed when any of the following conditions are met:
	- A PowerShell script or a proactive remediation is assigned to the user or device.
	- A Win32 app or Microsoft Store app is deployed.
	- A custom compliance policy is assigned.
- Windows custom compliance and WSL compliance settings must be configured in separate compliance policies.

## Before you begin

1. Ensure that you have unassigned and removed any existing custom compliance policy for WSL.
2. Review the [Limitations](./#Limitations) of using WSL settings in compliance policies.

## Add Intune WSL plug-in as a win32 app   

Create a Win32 app policy for the [Intune WSL plug-in](https://github.com/microsoft/shell-intune-samples/blame/master/Linux/WSL/IntuneWSLPluginInstaller/IntuneWSLPluginInstaller.msi) and assign it to the target Entra group.

1. Use the [Microsoft Win32 Content Prep Tool](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool) to convert the Intune WSL plug-in into the *.intunewin* format. For more information, see [Convert the Win32 app content](https://learn.microsoft.com/en-us/mem/intune/apps/apps-win32-prepare#convert-the-win32-app-content). 
   
2. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as at least a <insert least priveleged role>.  
   
3. Go to **Apps** > **All apps** > **Add**.  

4. For **App type**, scroll down to **Other**, and then select **Windows app (Win32)**.  

5. Choose **Select**. The **Add app** steps appear.  

6. Choose **Select app package file**.

7. Select the **Folder** button to browse your files for the app package file. Then choose the Intune WSL plug-in installation file with the `.intunewin` extension.   

8. Select **OK** to continue to the next step.  

9. Enter the following app information:  
   - **Select file**: The app package file you selected in the previous step appears here. Select the file to upload a different installation package file for the Intune WSL plug-in.   
   - **Name**: Enter **Intune WSL Plugin**.  
   - **Description**: Select **Edit Description** to enter a description for the app. For example, you can describe its purpose or how your organization plans to use it. This setting is optional but recommended.  
   - **Publisher**: Enter **Microsoft Intune**.  

10. Select **Next** to continue to **Program**.  

11. Review the settings that are prepopulated so that you are familiar with how the app behaves. You shouldn't need to change any of these settings.  

12. Select **Next** to go to **Requirements**.
13. Enter the requirements devices must meet to install the app.  

14. Select **Next** to go to **Detection rules**.
15. Review the detection rules that are prepopulated. These rules are app-specific and detect the presence of the app. You shouldn't need to change any of these settings.  

16. Select **Next** to go to **Dependencies**. Leave it as-is.

17. Select **Next** to go to **Supersedence**. Leave it as-is.

18. Select **Next** to go to **Assignments**.  

19. Add Microsoft Entra users under **Required** to assign the policy.  

20. Select **Next** to go to **Review + create**.  

21. Review the summary and then select **Create** to save the policy.  

> [!NOTE]
> Creating a compliance policy with WSL settings will automatically generate a read-only custom script. Editing the compliance policy will edit the associated custom script. These scripts appear under **Microsoft Intune admin center** > **Devices** > **Compliance** > **Scripts** and are named as _Built-in WSL Compliance-< compliance policy id >_.

## Limitations

The known limitations of using the Intune WSL plugin for compliance evaluation are as follows:

- Compliance evaluation requires that the installed Linux distributions in WSL have run at least once.
- Compliance evaluation is not guaranteed to function as expected on custom Linux images or Linux images without `etc/os-release` directory.
- The Intune WSL plugin cannot guarantee that malicious software or user actions have not compromised the compliance evaluation mechanism.

## Next steps

- [Create a compliance policy](create-compliance-policy.md#create-the-policy). For **Platform**, select **Windows 10 and later**. To learn about **Compliance settings** applicable to Windows Subsystem for Linux, see Device Compliance settings for [Windows Subsystem for Linux](compliance-policy-create-windows.md#windows-subsystem-for-linux-wsl).
- [Add actions for noncompliant devices](actions-for-noncompliance.md) and [use scope tags to filter policies](../fundamentals/scope-tags.md).
- [Monitor your compliance policies](compliance-policy-monitor.md).
- For WSL troubleshooting help, see [Windows Subsystem for Linux](/windows/wsl/troubleshooting).  
