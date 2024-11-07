---
# required metadata

title: Compliance for Windows Subsystem for Linux  
description: Evaluate WSL attributes on a host device for compliance. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 5/29/2024 
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

- [Intune WSL plug-in](https://github.com/microsoft/shell-intune-samples/tree/master/Linux/WSL/WSL%20Management%20Example) must be installed for compliance evaluation. 
- The Microsoft Intune management extension (IME) must be installed on the target device. This is automatically installed when any of the following conditions are met:
	- A PowerShell script or a proactive remediation is assigned to the user or device.
	- A Win32 app or Microsoft Store app is deployed.
	- A custom compliance policy is assigned.
- Windows custom compliance and WSL compliance settings must be configured in separate compliance policies.

## Before you begin

Ensure that you have unassigned and removed any existing custom compliance policy for WSL.

## Add Intune WSL plug-in as a win32 app   

Create a Win32 app policy for the [Intune WSL plug-in](https://github.com/microsoft/shell-intune-samples/tree/master/Linux/WSL/WSL%20Management%20Example) and assign it to the target Entra group.

1. Use the [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730) to convert the Intune WSL plug-in into the *.intunewin* format. [Learn more about converting to .intunewin format](https://learn.microsoft.com/en-us/mem/intune/apps/apps-win32-prepare#convert-the-win32-app-content).
   
2. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
   
3. Select **Apps** > **All apps** > **Add**.

4. On the **Select app type** pane, under the **Other** app types, select **Windows app (Win32)**.

5. Click **Select**. The **Add app** steps appear.

6. On the **Add app** pane, click **Select app package file**.

7. On the **App package file** pane, select the browse button. Then, select the converted Intune WSL plugin installation file with the extension _.intunewin_. 

8. When you're finished, select **OK** on the **App package file** pane.

9. Enter app information:  
   - **Select file**: Select this option to upload the installation package file for the Intune WSL plug-in.  
   - **Name**: Enter **Intune WSL Plugin**.  
   - **Description**: Enter a description for the app. This setting is optional but recommended. 
   - **Publisher**: Enter **Microsoft Intune**.  

10. Select **Next** to go to **Program**. Review the pre-populated settings. These shouldn't be changed.

11. Select **Next** to go to **Requirements**. Specify the requirements that devices must meet before the app is installed. 

12. Select **Next** to go to **Detection rules**. Review the pre-populated detection rules. These shouldn't be changed.

13. Select **Next** to go to **Dependencies**. Leave it as-is.

14. Select **Next** to go to **Supersedence**. Leave it as-is.

15. Select **Next** to go to **Assignments**.  

16. Add Microsoft Entra users under **Required** to assign the policy.  

17. Select **Next** to go to **Review + create**.  

18. Review the summary and then select **Create** to save the policy.  

> [!NOTE]
> Creating a compliance policy with WSL settings will automatically generate a read-only custom script. Editing the compliance policy will edit the associated custom script. These scripts appear under **Microsoft Intune admin center** > **Devices** > **Compliance** > **Scripts** and are named as _Built-in WSL Compliance-<compliance policy id>_.

## Next steps

- [Create a compliance policy](create-compliance-policy.md#create-the-policy). For **Platform**, select **Windows 10 and later**. To learn about **Compliance settings** applicable to Windows Subsystem for Linux, see Device Compliance settings for [Windows Subsystem for Linux](compliance-policy-create-windows.md#windows-subsystem-for-linux-wsl).
- [Add actions for noncompliant devices](actions-for-noncompliance.md) and [use scope tags to filter policies](../fundamentals/scope-tags.md).
- [Monitor your compliance policies](compliance-policy-monitor.md).
- For WSL troubleshooting help, see [Windows Subsystem for Linux](/windows/wsl/troubleshooting).  
