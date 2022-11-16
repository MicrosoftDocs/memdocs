---
# required metadata

title: Configure device configuration profiles 
titleSuffix: Microsoft Intune
description: Use Microsoft Intune to create email, VPN, and Wi-Fi device configuration profiles as part of the minimum set of policies for your devices.
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/15/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite:
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: 
  - M365-identity-device-management 
  - highpri
---

# Step 4: Create device configuration profiles to apply email, VPN and Wi-Fi connections

What is it?
Why do you need it?
How do you do it? Existing docs just to link to it


In this step, you are ready to configure features on your devices. When your devices enroll, these policies can be deployed during the enrollment process.

Ideally, you want your policy to be a minimum or baseline set of policies that all devices must have.

This articles applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

This article lists some common baselines device configuration policies that organizations use:

- Email
- VPN
- Wi-Fi

:::image type="content" source="./media/deployment-plan-configuration-profile/deploy-email-vpn-wifi.png" alt-text="Image that shows an email, VPN and Wi-Fi profiles deployed from Microsoft Intune to end user devices.":::

Most of these policies in this article focus on access to organization resources. In your organization, you may have a different set of baseline device configuration policies.

## Email

Many organizations deploy email profiles with preconfigured settings to end user devices.

✔️ **Automatically connect to user email accounts**

The profile includes the email configuration settings that automatically connect to your email server.

Depending on the settings you configure, the email profile can automatically connect the end users to their individual email account settings. End users don't have to manually configure their email accounts. 

✔️ **Access work or school email**

Creating an email profile is a common minimum baseline policy for organizations with users that use email on their devices.

Intune has built-in email settings for Android, iOS/iPadOS, and Windows client devices. When users open their email app, they can automatically connect, authenticate, and synchronize their organizational email accounts on their devices.

✔️ **Deploy anytime**

On new devices, it's recommended to deploy the email policy when devices enroll in Intune. If you have existing devices, you can deploy the email policy at any time.

### Get started with email profiles

To get started, use the following links:

?? Deploy an email app??

1. [Create an email configuration profile in Intune](../configuration/email-settings-configure.md).
2. Configure the settings for your platform:

    - [Android Enterprise email settings](../configuration/email-settings-android-enterprise.md)
    - [iOS/iPadOS email settings](../configuration/email-settings-ios.md)
    - [Windows email settings](../configuration/email-settings-windows-10.md)

3. [Assign the profile](../configuration/device-profile-assign.md) to your users or user groups.

## VPN

Many organizations deploy VPN profiles with preconfigured settings to end user devices. 

✔️ **Work from anywhere**

As end users work from anywhere, they can use the VPN profile to securely connect to their organization's network and access resources.

✔️ **Use Enterprise level VPN apps**

VPN profiles in Intune use common and popular VPN apps, such as Check Point, Cisco, Microsoft Tunnel, and more. The VPN app is deployed to end user devices. After the app is deployed, then you deploy the VPN connection profile with settings that configure the VPN app. The profile includes settings that automatically connect to your VPN server.

✔️ **Support remote workers**

Creating a VPN profile is a common minimum baseline policy for organizations with remote workers and hybrid workers.

Intune has built-in VPN settings for Android, iOS/iPadOS, macOS, and Windows client devices. On user devices, your VPN connection is shown as an available connection. Users select it. And, depending on the settings in your VPN profile, users can automatically authenticate and connect to the VPN on their devices.

✔️ **Deploy anytime**

On new devices, it's recommended to deploy the VPN app during the enrollment process. When enrollment completes, then deploy the VPN policy. If you have existing devices, deploy the VPN app at any time and then deploy the VPN policy.

### Get started with VPN profiles

To get started, use the following links:

1. Deploy a VPN app to your devices.

    - For a list of supported VPN apps, go to [Supported VPN connection apps in Intune](../configuration/vpn-settings-configure.md#vpn-connection-types).
    - For the steps to add apps to Intune, go to [Add apps to Microsoft Intune](../apps/apps-add.md).

2. [Create a VPN configuration profile in Intune](../configuration/vpn-settings-configure.md).
3. Configure the settings for your platform:

    - [Android Enterprise VPN settings](../configuration/vpn-settings-android-enterprise.md)
    - [iOS/iPadOS VPN settings](../configuration/vpn-settings-ios.md)
    - [macOS VPN settings](../configuration/vpn-settings-macos.md)
    - [Windows VPN settings](../configuration/vpn-settings-windows-10.md)

4. [Assign the profile](../configuration/device-profile-assign.md) to your users or user groups.

## Wi-Fi

Many organizations deploy Wi-Fi profiles with preconfigured settings to end user devices. 

✔️ **Connect wirelessly**

As end users work from different mobile devices, they can use the Wi-Fi profile to wirelessly and securely connect to your organization's network.

The profile includes the Wi-Fi configuration settings that automatically connect to your network and/or SSID (service set identifier). End users don't have to manually configure their Wi-Fi settings.

✔️ **Support mobile devices on-premises**

Creating a Wi-Fi profile is a common minimum baseline policy for organizations with mobile devices that work on-premises.

Intune has built-in Wi-Fi settings for Android, iOS/iPadOS, macOS, and Windows client devices. On user devices, your Wi-Fi connection is shown as an available connection. Users select it. And, depending on the settings in your Wi-Fi profile, users can automatically authenticate and connect to the Wi-Fi on their devices.

✔️ **Deploy anytime**

On new devices, it's recommended to deploy the Wi-Fi policy when devices enroll in Intune. If you have existing devices, you can deploy the Wi-Fi policy at any time.

### Get started with Wi-Fi profiles

To get started, use the following links:

1. [Create a Wi-Fi configuration profile in Intune](../configuration/wi-fi-settings-configure.md).
2. Configure the settings for your platform:

    - [Android Enterprise Wi-Fi settings](../configuration/wi-fi-settings-android-enterprise.md)
    - [iOS/iPadOS Wi-Fi settings](../configuration/wi-fi-settings-ios.md)
    - [macOS Wi-Fi settings](../configuration/wi-fi-settings-macos.md)
    - [Windows Wi-Fi settings](../configuration/vpn-settings-windows-10.md)

3. [Assign the profile](../configuration/device-profile-assign.md) to your users or user groups.

## Do more

### Settings catalog?

## Next steps

