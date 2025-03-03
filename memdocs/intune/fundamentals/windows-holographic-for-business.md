---
# required metadata
title: Use Windows Holographic devices with Microsoft Intune
description: Use Microsoft Intune to manage and complete different tasks on devices running Windows Holographic for Business and HoloLens. You can configure the Company Portal app, create a compliance policy, customize OMA-URI settings, deploy apps, categorize devices in groups, create profiles, restrict devices, enable software updates, set terms and conditions, configure VPN and Wi-Fi settings, and use Hello for Business.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/19/2024
ms.topic: article
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 585a2f17-106b-4f02-adf7-05f08a92dbc1
# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Manage and use different device management features on Windows Holographic and HoloLens devices with Intune

Microsoft Intune includes many features to help manage devices that run Windows Holographic for Business, like the [Microsoft HoloLens](/hololens/). Using Intune, you can confirm that devices are compliant with your organization's rules, and you can customize the device by adding a VPN or WiFi profile. Another key feature is to use the device as a Kiosk, and run a specific app, or a specific set of apps.

The tasks in this article help you manage, customize, and secure your devices running Windows Holographic for Business, including software updates and using Windows Hello for Business.

To use Windows Holographic devices with Intune, create an [Edition Upgrade](../configuration/edition-upgrade-configure-windows-10.md) profile. This upgrade profile upgrades the devices from Windows Holographic to Windows Holographic for Business. For the Microsoft HoloLens, you can buy the Commercial Suite to get the required license for the upgrade. For more information, go to [Upgrade devices running Windows Holographic to Windows Holographic for Business](../configuration/holographic-upgrade.md).

This article describes the different features and services you can use to manage devices running Windows Holographic for Business.

## Microsoft Entra ID

Microsoft Entra ID helps manage and control your devices running Windows Holographic for Business. When you use Intune and Microsoft Entra ID, you can:

- **[Join devices to Microsoft Entra ID](/entra/identity/devices/device-join-plan)**: In Microsoft Entra ID, you can add your work-owned Windows 10/11 devices, including devices running Windows Holographic for Business. This feature allows Microsoft Entra ID to control the device. It helps confirm that users are accessing the company resources from devices that meet your security and compliance standards.

  For information, go to [Device identity in Microsoft Entra ID](/entra/identity/devices/overview).

- **[Bulk enrollment for Windows devices](../enrollment/windows-bulk-enroll.md)**: You can join large numbers of new Windows devices to Microsoft Entra ID and Intune. This feature is called bulk enrollment, and uses provisioning packages. These packages join the devices running Windows Holographic for Business to your Microsoft Entra tenant, and enrolls them in Intune.

## Company Portal app

**[Configure the Company Portal app](../apps/company-portal-app.md)**.

Intune provides the Company Portal app for users to access company data, enroll devices, install apps, contact their IT department, and more. You can customize the Company Portal app for your devices running Windows Holographic for Business.

In the Company Portal app, end users can run the following actions:

- [Remove a device from Intune](../user-help/unenroll-your-device-from-intune-windows.md) using the Settings app or the Company Portal app
- [Rename a device](../user-help/rename-your-device-cpapp.md)
- [Install apps](../user-help/install-apps-cpapp-windows.md) on a device
- [Sync devices manually](../user-help/sync-your-device-manually-windows.md) from the Settings app or the Company Portal app

## Compliance policy

**[Create a device compliance policy](../protect/compliance-policy-create-windows.md)**.

Compliance policies are rules and settings that devices must meet to be compliant. Use these policies with Conditional Access to block access to company resources for devices that are noncompliant. In Intune, create compliance policies to allow or block access for devices running Windows Holographic for Business. For example, you can create a policy that requires BitLocker.

For more information, go to **[Get started with compliance policies](../protect/device-compliance-get-started.md)**.

## Deploy and manage apps

**[Add apps to Intune](../apps/apps-add.md)**.

Using Intune, you can add apps to your devices running Windows Holographic for Business. There are many ways to deploy apps, including:

- [Add Microsoft Store apps](../apps/store-apps-windows.md)
- [Add line-of-business (LOB) you create](../apps/lob-apps-windows.md)
- [Assign apps to groups](../apps/apps-deploy.md)

Microsoft Intune can deploy Universal Windows Apps (UWP) to Microsoft HoloLens devices running Windows Holographic for Business. You can directly upload and deploy your app packages using the Intune admin center. For more information, go to:

- To deploy Line-of-Business (LOB) apps using the Intune admin center, go to [How to add Windows line-of-business apps to Microsoft Intune](../apps/lob-apps-windows.md).

  > [!NOTE]
  > Intune allows a maximum package size to 8 GB. This package size is only available for the LOB apps uploaded to Intune.

- To learn about app management with Microsoft Intune, go to [What is app management in Microsoft Intune](../apps/app-management.md).
- To learn more about developing apps for Microsoft HoloLens, go to [Mixed reality apps for Microsoft HoloLens](https://www.microsoft.com/hololens/apps).

> [!NOTE]
> HoloLens devices running Windows 10 Holographic for Business 1607 don't support online-licensed apps from the Microsoft Store for Business. To learn more, go to [Install apps on HoloLens](/hololens/holographic-store-apps).

## Device actions

Intune has some built-in actions that allow IT admins to do different tasks locally on the device, or remotely using the Intune admin center. Users can also issue a remote command from the Intune Company Portal app to personally owned devices that are enrolled in Intune.

When you manage devices running Windows Holographic for Business, the following remote actions can be used:

- **[Wipe](../remote-actions/devices-wipe.md#wipe)**: The **Wipe** action removes the device from Intune, and restores the device back to its factory default settings. Use this action before giving the device to a new user, or when the device is lost or stolen.

- **[Retire](../remote-actions/devices-wipe.md#retire)**: The **Retire** action removes the device from Intune. It also removes managed app data, settings, and email profiles assigned by Intune. The user's personal data stays on the device.

- **[Sync devices to get the latest policies and actions](../remote-actions/device-sync.md)**: The **Sync** action forces the device to immediately check in with Intune. When a device checks in, the device receives any pending actions or policies that are assigned. This feature helps you validate and troubleshoot policies you assigned, without waiting for the next scheduled check-in.

For information about managing devices using the Intune admin center, go to [What is Microsoft Intune device management?](../remote-actions/device-management.md).

## Device categories and groups

**[Categorize devices into groups](../enrollment/device-group-mapping.md)**.

Using Intune, you can create device categories to automatically add devices to groups based on categories that you create, like Sales, Accounting, and Human Resources. The idea is to make it easier to manage your devices running Windows Holographic for Business.

## Device configuration profiles

**[Get started with configuration profiles](../configuration/device-profiles.md) and [profile overview](../configuration/device-profile-create.md)**.

Intune includes settings and features that you can enable or disable on different devices within your organization. These settings and features are managed using configuration profiles. For example, you can create a profile that uses Microsoft Defender Smart Screen on your devices running Windows Holographic for Business.

In your profiles, you can use OMA-URI to customize some settings, create device restrictions, and configure a virtual private network (VPN) and Wi-Fi.

### [Custom device settings](../configuration/custom-settings-windows-holographic.md)

To configure OMA-URI (Open Mobile Alliance Uniform Resource Identifier) settings, you can create a custom profile in Intune. Use the OMA-URI settings to control different features on your Windows Holographic for Business devices. Typically, custom profiles are used to configure settings that aren't built-in to Intune.

The [HoloLens 2 devices example](../configuration/custom-profile-hololens.md) uses the [Windows Defender Application Control (WDAC) CSP](/windows/client-management/mdm/applicationcontrol-csp) to allow or block apps from opening on HoloLens 2 devices.

### [Configure kiosk mode](../configuration/kiosk-settings-holographic.md)

Using the shared or guest PC features available in Intune, you can configure Windows Holographic for Business devices to run as a kiosk. These devices can run one app (single-app kiosk mode), or run many apps (multi-app kiosk mode).

### [Device restrictions](../configuration/device-restrictions-windows-holographic.md)

Device restrictions let you control different settings and features on your devices. For example, you can require a password, install apps from [Microsoft Store](https://www.microsoft.com/store/apps/windows?icid=CNavAppsWindowsApps), and enable Bluetooth. These restrictions are created in an Intune configuration profile. This profile can be applied to multiple devices running Windows Holographic for Business.

### [Configure VPN](../configuration/vpn-settings-configure.md)

Virtual private networks (VPNs) give your users secure remote access to your organization network. In Intune, you can create a VPN profile that includes specific settings for your devices running Windows Holographic for Business. For example, you can create a VPN profile so all Windows Holographic for Business devices use Citrix VPN as the connection type.

> [!NOTE]
> When assigning a VPN policy to Windows Holographic for Business devices, assign the profile to the device scope. Currently, Windows Holographic only supports the device scope. When the VPN profile is installed in the device context, it applies to all users on the device. If a user profile is deployed, it's treated as a device profile.

### [Configure Wi-Fi](../configuration/wi-fi-settings-configure.md)

You can also create a Wi-Fi profile in Intune to assign wireless network settings to your Windows Holographic for Business devices. When you assign a Wi-Fi profile, your end users get corporate network access, without any network configuration. For example, you can create a Wi-Fi network dedicated to only your Windows Holographic for Business devices.

## Shared multi-user devices

Devices that run Windows Holographic for Business, like the Microsoft HoloLens, can have multiple users. Intune includes settings to control different features on these shared devices, like power management, using the local storage, and account management. The configuration profiles can also be applied to devices with different operating systems.

For more information, go to [Shared devices](../configuration/shared-user-device-settings-windows-holographic.md).

## Software updates

**[Manage software updates](../protect/windows-update-for-business-configure.md)**.

Intune has different feature that focus on updating Windows client devices. These options include that determine how updates are installed. For example, you can create a maintenance window to install updates, or choose to restart after updates are installed. Updates can be applied to multiple devices running Windows Holographic for Business.

## Terms and conditions

**[Set your company's terms and conditions for user access](../enrollment/terms-and-conditions-create.md)**.

Before users enroll devices and access your company apps, including email, you can require that users accept your company's terms and conditions. In Intune, define how the terms and conditions are shown in the Company Portal app, and also assign these terms and conditions to devices running Windows Holographic for Business.

## Windows Hello for Business

**[Use Windows Hello for Business](../protect/windows-hello.md)**.

Hello for Business is an alternative sign-in method that uses a Microsoft Entra account to replace a password, smart card, or a virtual smart card. With Hello for Business, your Windows Holographic for Business devices can sign in with a PIN with a minimum length set by you.

## Related content

[Set up Intune](deployment-plan-setup.md).
