---
# required metadata
title: Windows 365 Boot physical device requirements
titleSuffix:
description: Get your physical devices prepared for Windows 365 Boot.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/05/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: elluthra
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started; intro-overview
ms.collection:
- M365-identity-device-management
- tier2
---

# Windows 365 Boot physical device setup and requirements

Follow these steps and requirements to set up shared physical devices for Windows 365 Boot.

## Operating system requirements

Each physical device (and Cloud PC) must be running one of the following, version 22621.3374 or later: 

- Windows 11 Enterprise
- Windows 11 Professional
- Windows IoT Enterprise

## Configure the physical device

1. Open **Windows Update** and turn on **Get the latest updates as soon as they’re available**.
2. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices**.
3. Select the device in the list > **Wipe** > **Wipe**. Don't select any of the boxes in the wipe confirmation box.
4. The next time the device connects to the internet, it will be wiped. This process can take several minutes.
5. Complete the Windows Autopilot steps in the next section.

## Register the physical device with Windows Autopilot

If the device is already registered with Autopilot, skip this section.

1. At the physical device's sign-in prompt, use Shift+F10 to open a command prompt.
2. In the command prompt, run the following commands

   ```azurepowershell
   PowerShell.exe -ExecutionPolicy Bypass 
   [Net.ServicePointManager]::SecurityProtocol  = [Net.SecurityProtocolType]::Tls12 
   Install-Script -name Get-WindowsAutopilotInfo -Force 
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned 
   Get-WindowsAutopilotInfo -Online 
   ```

3. When prompted, sign in with a user that has the Intune Administrator role. After sign-in, the device is automatically enrolled in Intune. Make a note of the serial number.

<a name='add-the-physical-device-to-the-azure-active-directory-group'></a>

## Add the physical device to the Microsoft Entra group

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as a user with the Intune Service Administrator role.
2. Select **Groups** > **All groups** > search for the Microsoft Entra group that you used in the [Windows 365 Boot guided scenario](windows-365-boot-guide.md) > select the group.
3. On the group page, select **Members** > **Add members** > search physical device's serial number > select the physical device > **Select**.
4. Wait several minutes while the resource assignments complete.

During this time, review your other device configurations that may apply to the device. Make sure that they're appropriate for a device that only directly connects to a Windows 365 Cloud PC. Unassign unnecessary apps and configuration profiles to make sure the Windows 365 Boot connection is a seamless connection experience. Also see [Restrict user access to Windows 365 Boot physical devices](windows-365-boot-restrict-user-access-physical-device.md).

## Sign in to the device

1. Complete the Out-of-Box-Experience (OOBE) for the physical device as you would with any user.
2. After OOBE, restart the device.
3. When the user signs in to the device, they're taken directly to their Windows 365 Cloud PC.

<!-- ########################## -->
## Next steps

[Restrict user access to Windows 365 Boot physical devices](windows-365-boot-restrict-user-access-physical-device.md)

[Troubleshoot Windows 365 Boot](troubleshoot-windows-365-boot.md).
