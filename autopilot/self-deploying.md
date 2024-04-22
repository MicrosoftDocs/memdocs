---
title: Windows Autopilot self-deploying mode
description: Self-deploying mode allows a device to be deployed with little to no user interaction. This mode is designed to deploy Windows as a kiosk, digital signage device, or a shared device.
ms.subservice: itpro-deploy
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/16/2024
ms.collection:
  - M365-modern-desktop
  - highpri
  - tier1
ms.topic: how-to
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a>
---

# Windows Autopilot self-deploying mode

> [!NOTE]
>
> For more information about using Windows Autopilot to deploy HoloLens 2 devices, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot).

> [!TIP]
>
> For a guided walkthrough of Windows Autopilot self-deploying mode, see [Step by step tutorial for Windows Autopilot self-deploying mode in Intune](tutorial/self-deploying/self-deploying-workflow.md).

Windows Autopilot self-deploying mode lets you deploy a device with little to no user interaction. For devices with an Ethernet connection, no user interaction is required. For devices connected via Wi-Fi, the user must only:

- Choose the language, locale, and keyboard.
- Make a network connection.

Self-deploying mode provides all the following features:

- Joins the device to Microsoft Entra ID.
- Enrolls the device in Intune or another mobile device management (MDM) service using Microsoft Entra ID for automatic MDM enrollment.
- Makes sure that all policies, applications, certificates, and networking profiles are provisioned on the device.
- Uses the Enrollment Status Page to prevent access until the device is fully provisioned.

> [!NOTE]
>
> Autopilot self-deploying mode is only supported for Microsoft Entra join devices. Autopilot self-deploying mode isn't supported for Microsoft Entra hybrid join devices.

Self-deploying mode lets you deploy a Windows device as a kiosk, digital signage device, or a shared device.

Autopilot now has a kiosk mode that supports Kiosk Browser, Microsoft Store apps, and specific versions of Microsoft Edge.

You can use the [Kiosk Browser](https://www.microsoft.com/p/kiosk-browser/9ngb5s5xg2kp?rtc=1&activetab=pivot:overviewtab) when setting up a kiosk device. This app is built on Microsoft Edge and can be used to create a tailored, MDM-managed browsing experience.

You can completely automate device configuration by combining self-deploying mode with MDM policies. Use the MDM policies to create a local account configured to automatically sign in. For more information, see:

- [Simplifying kiosk management for IT with Windows 10](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/simplifying-kiosk-management-for-it-with-windows-10/ba-p/187691).
- [Set up a kiosk or digital sign in Intune or other MDM service](/windows/configuration/setup-kiosk-digital-signage#set-up-a-kiosk-or-digital-sign-in-intune-or-other-mdm-service).

Optionally, you can use a [device-only subscription](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/microsoft-intune-announces-device-only-subscription-for-shared/ba-p/280817) service that helps manage devices that aren't affiliated with specific users. The Intune device SKU is licensed per device per month.

> [!NOTE]
>
> Intune doesn't automatically configure a primary user when you use self-deploying mode in Autopilot to provision a Windows device. Some Intune capabilities rely on a primary user being set on a device (which you can [manually do in the Intune admin center](/mem/intune/remote-actions/find-primary-user#change-a-devices-primary-user) after device provisioning if desired). These features include user self-service BitLocker recovery key retrieval and using the Company Portal to install software. Using self-provisioning mode for Autopilot doesn't preclude a licensed user from logging into the device and using features entitled to that user such as conditional access. For more information, see [Windows Autopilot scenarios and capabilities](windows-autopilot-scenarios.md).

## Requirements

> [!IMPORTANT]
>
> You can't automatically re-enroll a device through Autopilot after an initial deployment in self-deploying mode. Instead, delete the device record in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). From the admin center, select **Devices** > **All devices** > select the devices you want to delete > **Delete**.  For more information, see [Updates to the Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/updates-to-the-windows-autopilot-sign-in-and-deployment/ba-p/2848452).

Self-deploying mode uses a device's Trusted Platform Module (TPM) 2.0 hardware to authenticate the device into an organization's Microsoft Entra tenant. Therefore, devices without TPM 2.0 can't be used with this mode. Devices must also support TPM device attestation. All new Windows devices should meet these requirements. The TPM attestation process also requires access to a set of HTTPS URLs that are unique for each TPM provider. For more information, see the entry for Autopilot self-Deploying mode and Autopilot pre-provisioning in [Networking requirements](networking-requirements.md#tpm). For Windows Autopilot software requirements, see [Windows Autopilot software requirements](./software-requirements.md).

> [!IMPORTANT]
>
> If you attempt a self-deploying mode deployment on a device that doesn't have support TPM 2.0 or on a virtual machine, the process fails when verifying the device with an **0x800705B4** timeout error. This includes Hyper-V virtual TPMs.
>
> See [Windows Autopilot known issues](known-issues.md) and [Troubleshoot Autopilot device import and enrollment](troubleshoot-device-enrollment.md) to review other known errors and solutions.

You can display an organization-specific logo and organization name during the Autopilot process. To do so, Microsoft Entra Company Branding must be configured with the images and text you want displayed. See [Quickstart: Add company branding to your sign-in page in Microsoft Entra ID](/azure/active-directory/fundamentals/customize-branding) for more details.

## Step by step

To deploy in self-deploying mode Windows Autopilot, the following preparation steps need to be completed:

1. Create an Autopilot profile for self-deploying mode with the settings you want. In Microsoft Intune, this mode is explicitly chosen when creating the profile. It isn't possible to create a profile in the Microsoft Store for Business or Partner Center for self-deploying mode.

1. If using Intune, create a device group in Microsoft Entra ID and assign the Autopilot profile to that group. Ensure that the profile is assigned to the device before attempting to deploy that device.

1. Boot the device, connecting it to Wi-Fi if necessary, then wait for the provisioning process to complete.

## Validation

When using Windows Autopilot to deploy in self-deploying mode, the following end-user experience should be observed:

- Once the device connects to a network, the Autopilot profile is downloaded.

- If connected to Ethernet, and the Autopilot profile is configured to skip them, the following pages aren't displayed:

  - Language and locale.
  - Keyboard layout.

  Otherwise, manual steps are required:

  - If multiple languages are preinstalled in Windows, the user must pick a language.
  - The user must pick a locale and a keyboard layout, and optionally a second keyboard layout.

- If connected via Ethernet, no network prompt is expected. If no Ethernet connection is available and Wi-Fi is built in, the user needs to connect to a wireless network.

- Windows checks for critical out-of-box experience (OOBE) updates, and if any are available they're automatically installed, rebooting if necessary.

- The device joins Microsoft Entra ID.

- The device enrolls in Intune or other configured MDM services after it joins Microsoft Entra ID.

- The [enrollment status page](enrollment-status.md) is displayed.

- Depending on the device settings deployed, the device will either:

  - Remain at the sign-on screen, where any member of the organization can sign in by specifying their Microsoft Entra credentials.
  - Automatically sign in as a local account, for devices configured as a kiosk or digital signage.

>[!NOTE]
>
> Deploying Exchange ActiveSync (EAS) policies using self-deploying mode for kiosk deployments causes autologon functionality to fail.

In case the observed results don't match these expectations, consult the [Windows Autopilot Troubleshooting](troubleshooting.md) documentation.
