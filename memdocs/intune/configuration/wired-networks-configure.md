---
# required metadata

title: Configure 802.1x wired network settings for macOS devices in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Create or add a wired network device configuration profile for macOS desktop computer devices. See the different settings, add certificates, choose an EAP type, and select an authentication method in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/29/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add and use wired networks settings on your macOS devices in Microsoft Intune

Wired networks are used by many organizations to give network access to desktop computers. Microsoft Intune includes built-in settings that can be deployed to macOS users and devices in your organization. This group of settings is called a "profile". In your profile, you can include common settings, such as the network interface, accepted EAP types, and server trust settings.

When the profile is ready, it can be assigned to different users and groups. Once assigned, your users get access your organization's wired network without configuring it themselves.

As part of your mobile device management (MDM) solution, use this feature to create 802.1x profiles to manage wired networks. Then, deploy these wired networks to your macOS devices.

This feature applies to:

- macOS

For example, you have a wired network named **Contoso wired network**. You want to set up all macOS desktops to connect to this network. Here's the process:

1. Create a wired network profile that includes the settings that connect to the **Contoso wired network**.
2. Assign the profile to a group that includes all users macOS desktop computers. For recommendations on using group types, see [User groups vs. device groups](device-profile-assign.md#user-groups-vs-device-groups).
3. On their desktops, users find the **Contoso wired network** in the list of networks. They can then connect to the network, using the authentication method of your choosing.

This article lists the steps to create a wired network profile. It also includes a link that describes the different settings.

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **macOS**.
    - **Profile**: Select **Templates** > **Wired Network**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **macOS: Wired network for entire company**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, select the network interface of the network, and choose the Extensible Authentication Protocol (EAP) type. For a list of all settings, and what they do, see:

    - [macOS](wired-network-settings-macos.md)

8. Select **Next**.
9. In **Assignments**, select the user groups or device groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

10. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

> [!TIP]
> If you use certificate based authentication for your wired network profile, then deploy the wired network profile, certificate profile, and trusted root profile to the same groups. This deployment makes sure that each device can recognize the legitimacy of your certificate authority. For more information, see [configure certificates with Microsoft Intune](../protect/certificates-configure.md).

## Next steps

The profile is created, but may not be doing anything. Be sure to [assign this profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).
