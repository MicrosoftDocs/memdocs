---
# required metadata
title: Use Windows Holographic devices with Microsoft Intune
description: Using Microsoft Intune, you can manage and complete different tasks on devices running Windows Holographic for Business and HoloLens, including configure the Company Portal, create a compliance policy, customize OMA-URI settings, deploy apps, categorize devices in groups, create profiles, restrict devices, enable software updates, set terms and conditions, configure VPN and Wi-Fi settings, and use Hello for Business.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/24/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 585a2f17-106b-4f02-adf7-05f08a92dbc1
# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure, seodec18
ms.collection: M365-identity-device-management
---

# Manage and use different device management features on Windows Holographic and HoloLens devices with Intune

Microsoft Intune includes many features to help manage devices that run Windows Holographic for Business, such as the [Microsoft HoloLens](/hololens/). Using Intune, you can confirm that devices are compliant with your organization's rules, and you can customize the device by adding a VPN or WiFi profile. Another key feature is to use the device as a Kiosk, and run a specific app, or a specific set of apps.

The tasks in this article help you manage, customize, and secure your devices running Windows Holographic for Business, including software updates and using Windows Hello for Business.

To use Windows Holographic devices with Intune, create an Edition Upgrade profile. This upgrade profile upgrades the devices from Windows Holographic to Windows Holographic for Business. For the Microsoft HoloLens, you can buy the Commercial Suite to get the required license for the upgrade. For more information, see [Upgrade devices running Windows Holographic to Windows Holographic for Business](../configuration/holographic-upgrade.md).

## Azure Active Directory

Azure Active Directory (AD) is a great resource to help manage and control your devices running Windows Holographic for Business. Using Intune and Azure AD, you can: 

- **[Join devices to Azure Active Directory](/azure/active-directory/devices/azureadjoin-plan)**: In Azure Active Directory (AD), you can add your work-owned Windows 10/11 devices, including devices running Windows Holographic for Business. This feature allows Azure AD to control the device. It helps confirm that users are accessing the company resources from devices that meet your security and compliance standards.

  [Device management in Azure AD](/azure/active-directory/devices/overview) provides more details.

- **[Bulk enrollment for Windows devices](../enrollment/windows-bulk-enroll.md)**: You can join large numbers of new Windows devices to Azure Active Directory (AD) and Intune. This feature is called bulk enrollment, and uses provisioning packages. These packages join the devices running Windows Holographic for Business to your Azure AD tenant, and enrolls them in Intune.

## Company Portal

**[Configure the Company Portal app](../apps/company-portal-app.md)**

Intune provides the Company Portal app for users to access company data, enroll devices, install apps, contact their IT department, and more. You can customize the Company Portal app for your devices running Windows Holographic for Business.

Using the Company Portal app, you can also run the following actions:

- [Remove a device from Intune](../user-help/unenroll-your-device-from-intune-windows.md) using the Settings app or the Company Portal app
- [Rename a device](../user-help/rename-your-device-cpapp.md)
- [Install apps](../user-help/install-apps-cpapp-windows.md) on a device
- [Sync devices manually](../user-help/sync-your-device-manually-windows.md) from the Settings app or the Company Portal app

## Compliance policy

**[Create a device compliance policy](../protect/compliance-policy-create-windows.md)**

Compliance policies are rules and settings that devices must meet to be compliant. Use these policies with Conditional Access to block access to company resources for devices that are not-compliant. In Intune, create compliance policies to allow or block access for devices running Windows Holographic for Business. For example, you can create a policy that requires BitLocker be enabled.

See also **[Get started with compliance policies](../protect/device-compliance-get-started.md)**.

## Deploy and manage apps

**[Add apps to Intune](../apps/apps-add.md)**

Using Intune, you can add apps to your devices running Windows Holographic for Business. There are many ways to deploy apps, including:

- [Add Microsoft Store apps](../apps/store-apps-windows.md)
- [Add apps you create](../apps/lob-apps-windows.md)
- [Assign apps to groups](../apps/apps-deploy.md)

Microsoft Intune can deploy Universal Windows Apps to Microsoft HoloLens devices running Windows Holographic for Business. You can directly upload your app packages in the Intune Azure portal, or deploy them from the Microsoft Store for Business. For more information about related areas, see the following articles:
- To deploy Line-of-Business (LOB) apps using the Intune Azure portal, see [How to add Windows line-of-business apps to Microsoft Intune](../apps/lob-apps-windows.md).

    > [!NOTE]
    > Intune allows a maximum package size to 8 GB. This package size is only available for the LOB apps uploaded to Intune.

- To deploy apps using the Microsoft Store for Business, see [How to manage apps you purchased from the Microsoft Store for Business with Microsoft Intune](../apps/windows-store-for-business.md). 
- To learn about app management with Microsoft Intune, see [What is app management in Microsoft Intune](../apps/app-management.md).
- To learn more about developing apps for Microsoft HoloLens, see [Mixed reality apps for Microsoft HoloLens](https://www.microsoft.com/hololens/apps). 

> [!NOTE]
> HoloLens devices running Windows 10 Holographic for Business 1607 don't support online-licensed apps from the Microsoft Store for Business. To learn more, see [Install apps on HoloLens](/hololens/holographic-store-apps).

## Device actions

Intune has some built-in actions that allow IT administrators to do different tasks, locally on the device, or remotely using Intune in the Azure portal. Users can also issue a remote command from the Intune Company Portal to personally owned devices that are enrolled in Intune.

When using devices running Windows Holographic for Business, the following actions can be used: 

- **[Wipe](../remote-actions/devices-wipe.md#wipe)**: The **Wipe** action removes the device from Intune, and restores the device back to its factory default settings. Use this action before giving the device to a new user, or when the device is lost or stolen.

- **[Retire](../remote-actions/devices-wipe.md#retire)**: The **Retire** action removes the device from Intune. It also removes managed app data, settings, and email profiles assigned by Intune. The user's personal data stays on the device.

- **[Sync devices to get the latest policies and actions](../remote-actions/device-sync.md)**: The **Sync** action forces the device to immediately check in with Intune. When a device checks in, the device immediately receives any pending actions or policies that are assigned. This feature helps you validate and troubleshoot policies you've assigned, without waiting for the next scheduled check-in.

**[What is Microsoft Intune device management?](../remote-actions/device-management.md)** is a good resource to learn about managing devices using the Azure portal. 

## Device categories and groups

**[Categorize devices into groups](../enrollment/device-group-mapping.md)**

Using Intune, you can create device categories to automatically add devices to groups based on categories that you create, such as Sales, Accounting, Human Resources, and so on. The idea is to make it easier to manage your devices running Windows Holographic for Business.

## Device configuration profiles

**[Get started with configuration profiles](../configuration/device-profiles.md), and [profile overview](../configuration/device-profile-create.md)**

Intune includes settings and features that you can enable or disable on different devices within your organization. These settings and features are managed using profiles. For example, you can create a profile that enables Cortana, or uses Microsoft Defender Smart Screen on your devices running Windows Holographic for Business.

In your profiles, you can use OMA-URI to customize some settings, create device restrictions, and configure a virtual private network (VPN) and Wi-Fi.

### [Custom device settings](../configuration/custom-settings-windows-holographic.md)

To configure OMA-URI (Open Mobile Alliance Uniform Resource Identifier) settings, you can create a custom profile in Intune. Use the OMA-URI settings to control different features on your Windows Holographic for Business devices, such as enabling VPN, or checking for updates on Microsoft Update.

See an [example](../configuration/custom-profile-hololens.md) that uses the [Windows Defender Application Control (WDAC) CSP](/windows/client-management/mdm/applicationcontrol-csp) to allow or block apps from opening on HoloLens 2 devices.

### [Configure kiosk mode](../configuration/kiosk-settings-holographic.md)

Using the shared or guest PC features available in Intune, you can configure Windows Holographic for Business devices to run as a kiosk. These devices can run one app (single-app kiosk mode), or run multiple apps (multi-app kiosk mode).

### [Device restrictions](../configuration/device-restrictions-windows-holographic.md)

Device restrictions let you control different settings and features on your devices, including requiring a password, installing apps from [Microsoft Store](https://www.microsoft.com/store/apps/windows?icid=CNavAppsWindowsApps), enabling Bluetooth, and more. These restrictions are created in an Intune profile. This profile can be applied to multiple devices running Windows Holographic for Business.

### [Configure VPN](../configuration/vpn-settings-configure.md)

Virtual private networks (VPNs) give your users secure remote access to your company network. In Intune, you can create a VPN profile that includes specific settings for your devices running Windows Holographic for Business. For example, you can create a VPN profile so all Windows Holographic for Business devices use Citrix VPN as the connection type.

### [Configure Wi-Fi](../configuration/wi-fi-settings-configure.md)

You can also create a Wi-Fi profile in Intune to assign wireless network settings to your Windows Holographic for Business devices. When you assign a Wi-Fi profile, your end users get corporate network access, without any network configuration. For example, you can create a Wi-Fi network dedicated to only your Windows Holographic for Business devices.

## Shared multi-user devices

[Shared devices](../configuration/shared-user-device-settings-windows-holographic.md)

Devices that run Windows Holographic for Business, such as the Microsoft HoloLens, can have multiple users. Intune includes settings to control different features on these shared devices, such as power management, using the local storage, and account management. The configuration profiles can also be applied to devices with different operating systems. For example, the devices group can have devices that run RS2 and RS3 in the same group.

## Software updates

**[Manage software updates](../protect/windows-update-for-business-configure.md)**

Intune includes a feature called update rings for Windows client devices. These update rings include a group of settings that determine how updates are installed. For example, you can create a maintenance window to install updates, or choose to restart after updates are installed. An update ring can be applied to multiple devices running Windows Holographic for Business.

## Terms and conditions

**[Set your company's terms and conditions for user access](../enrollment/terms-and-conditions-create.md)**

Before users enroll devices and access your company apps, including email, you can require that users accept your company's terms and conditions. In Intune, define how the terms and conditions are shown in the Company Portal, and also assign these terms and conditions to devices running Windows Holographic for Business.

## Windows Hello for Business

**[Use Windows Hello for Business](../protect/windows-hello.md)**

Hello for Business is an alternative sign-in method that uses an Azure Active Directory account to replace a password, smart card, or a virtual smart card. With Hello for Business, your Windows Holographic for Business devices can sign in with a PIN with a minimum length set by you.

## Next steps

[Set up Intune](setup-steps.md).