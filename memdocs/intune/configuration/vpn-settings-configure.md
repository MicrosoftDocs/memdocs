---
# required metadata

title: Add VPN settings to devices in Microsoft Intune - Azure | Microsoft Docs
description: For Android, Android Enterprise, iOS, iPadOS, macOS, and Windows devices, use built-in settings to create virtual private network (VPN) connections in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Create VPN profiles to connect to VPN servers in Intune



Virtual private networks (VPNs) give your users secure remote access to your organization network. Devices use a VPN connection profile to start a connection with the VPN server. **VPN profiles** in Microsoft Intune assign VPN settings to users and devices in your organization, so they can easily and securely connect to your organizational network.

For example, you want to configure all iOS/iPadOS devices with the required settings to connect to a file share on the organization network. You create a VPN profile that includes these settings. Then, you assign this profile to all users who have iOS/iPadOS devices. The users see the VPN connection in the list of available networks, and can connect with minimal effort.

> [!NOTE]
> You can use [Intune custom configuration policies](custom-settings-configure.md) to create VPN profiles for the following platforms:
>
> * Android 4 and later
> * Enrolled devices that run Windows 8.1 and later
> * Windows Phone 8.1 and later
> * Enrolled devices that run Windows 10 desktop
> * Windows 10 Mobile
> * Windows Holographic for Business

## VPN connection types

You can create VPN profiles using the following connection types:

|Connection type|Platform|
|-|-|
|Automatic|Windows 10|
|Check Point Capsule VPN|- Android<br/>- Android Enterprise work profiles<br/>- iOS/iPadOS<br/>- macOS<br/>- Windows 10<br/>- Windows 8.1<br/>- Windows Phone 8.1|
|Cisco AnyConnect|- Android<br/>- Android Enterprise work profiles<br/>- Android Enterprise device owner (fully managed)<br/>- iOS/iPadOS<br/>- macOS|
|Cisco (IPSec)|iOS/iPadOS|
|Citrix SSO|- Android<br/>- Android Enterprise work profiles: Use [app configuration policy](../apps/app-configuration-policies-use-android.md)<br/>- Android Enterprise device owner (fully managed): Use [app configuration policy](../apps/app-configuration-policies-use-android.md)<br/>- iOS/iPadOS<br/>- Windows 10|
|Custom VPN|- iOS/iPadOS<br/>- macOS|
|F5 Access|- Android<br/>- Android Enterprise work profiles<br/>- Android Enterprise device owner (fully managed)<br/>- iOS/iPadOS<br/>- macOS<br/>- Windows 10<br/>- Windows 8.1<br/>- Windows Phone 8.1|
|IKEv2| - iOS/iPadOS<br/>- Windows 10|
|L2TP|Windows 10|
|Palo Alto Networks GlobalProtect|- Android Enterprise work profiles: Use [app configuration policy](../apps/app-configuration-policies-use-android.md)<br/>- iOS/iPadOS<br/>- Windows 10|
|PPTP|Windows 10|
|Pulse Secure|- Android<br/>- Android Enterprise work profiles<br/>- Android Enterprise device owner (fully managed)<br/>- iOS/iPadOS<br/>- macOS<br/>- Windows 10<br/>- Windows 8.1<br/>- Windows Phone 8.1|
|SonicWall Mobile Connect|- Android<br/>- Android Enterprise work profiles<br/>- iOS/iPadOS<br/>- macOS<br/>- Windows 10<br/>- Windows 8.1<br/>- Windows Phone 8.1|
|Zscaler|- Android Enterprise work profiles: Use [app configuration policy](../apps/app-configuration-policies-use-android.md)<br/>- iOS/iPadOS|

> [!IMPORTANT]
> Before you can use VPN profiles assigned to a device, you must install the applicable VPN app for the profile. You can use the information in the [What is app management in Microsoft Intune?](../apps/app-management.md) article to help you assign the app by using Intune.  

Learn how to  create custom VPN profiles by using URI settings in [Create a profile with custom settings](custom-settings-configure.md).

## Create a device profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **VPN profile for entire company**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
    - **Platform**: Choose the platform of your devices. Your options:

      - **Android**
      - **Android Enterprise** > **Device owner only**
      - **Android Enterprise** > **Work profile only**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows Phone 8.1**
      - **Windows 8.1 and later**
      - **Windows 10 and later**

    - **Profile type**: Select **VPN**.

4. Depending on the platform you chose, the settings you can configure are different. See the following articles for detailed settings on each platform:

    - [Android settings](vpn-settings-android.md)
    - [Android Enterprise settings](vpn-settings-android-enterprise.md)
    - [iOS/iPadOS settings](vpn-settings-ios.md)
    - [macOS settings](vpn-settings-macos.md)
    - [Windows Phone 8.1 settings](vpn-settings-windows-phone-8-1.md)
    - [Windows 8.1 settings](vpn-settings-windows-8-1.md)
    - [Windows 10 settings](vpn-settings-windows-10.md) (including Windows Holographic for Business)

5. When you're done, select **OK** > **Create** to save your changes.

The profile is created and appears on the profiles list. To assign this profile to groups, see [assign device profiles](device-profile-assign.md).

## Secure your VPN profiles

VPN profiles can use a number of different connection types and protocols from different manufacturers. These connections are typically secured through the following methods.

### Certificates

When you create the VPN profile, you choose a SCEP or PKCS certificate profile that you previously created in Intune. This profile is known as the identity certificate. It's used to authenticate against a trusted certificate profile (or *root certificate*) that you create to allow the user’s device to connect. The trusted certificate is assigned to the computer that authenticates the VPN connection, typically, the VPN server.

For more information about how to create and use certificate profiles in Intune, see [How to configure certificates with Microsoft Intune](../protect/certificates-configure.md).

### User name and password

The user authenticates to the VPN server by providing a user name and password.

## Next steps

Once the profile is created, it isn't doing anything yet. Next, [assign the profile](device-profile-assign.md) to some devices.

You can also create and use per-app VPNs on [Android](android-pulse-secure-per-app-vpn.md) and [iOS/iPadOS](vpn-setting-configure-per-app.md) devices.
