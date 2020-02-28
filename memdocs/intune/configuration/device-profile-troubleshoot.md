---
# required metadata

title: Troubleshoot device profiles in Microsoft Intune - Azure | Microsoft Docs
description: Common questions and answers with device policies and profiles, including profile changes not applied to users or devices, how long it takes for new policies to be pushed to devices, which settings are applied when there are multiple policies, what happens when a profile is deleted or removed, and more with Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Common questions, issues, and resolutions with device policies and profiles in Microsoft Intune

Get answers to common questions when working with device profiles and policies in Intune. This article also lists the check-in time intervals, provides more detains on conflicts, and more.

## Why doesn't a user get a new profile when changing a password or passphrase on an existing Wi-Fi profile?

You create a corporate Wi-Fi profile, deploy the profile to a group, change the password, and save the profile. When the profile changes, some users may not get the new profile.

To mitigate this issue, set up guest Wi-Fi. If the corporate Wi-Fi fails, users can connect to the guest Wi-Fi. Be sure to enable any automatically connect settings. Deploy the guest Wi-Fi profile to all users.

Some additional recommendations:  

- If the Wi-Fi network you're connecting to uses a password or passphrase, make sure you can connect to the Wi-Fi router directly. You can test with an iOS/iPadOS device.
- After you successfully connect to the Wi-Fi endpoint (Wi-Fi router), note the SSID and the credential used (this value is the password or passphrase).
- Enter the SSID and credential (password or passphrase) in the Pre-Shared Key field. 
- Deploy to a test group that has limited number of users, preferably only the IT team. 
- Sync your iOS/iPadOS device to Intune. Enroll if you haven’t already enrolled. 
- Test connecting to the same Wi-Fi endpoint (as mentioned in the first step) again.
- Roll out to larger groups and eventually to all expected users in your organization. 

## How long does it take for devices to get a policy, profile, or app after they are assigned?

Intune notifies the device to check in with the Intune service. The notification times vary, including immediately up to a few hours. These notification times also vary between platforms.

If a device doesn't check in to get the policy or profile after the first notification, Intune makes three more attempts. An offline device, such as turned off, or not connected to a network, may not receive the notifications. In this case, the device gets the policy or profile on its next scheduled check-in with the Intune service. The same applies to checks for non-compliance, including devices that move from a compliant to a non-compliant state.

**Estimated** frequencies:

| Platform | Refresh cycle|
| --- | --- |
| iOS/iPadOS | About every 8 hours |
| macOS | About every 8 hours |
| Android | About every 8 hours |
| Windows 10 PCs enrolled as devices | About every 8 hours |
| Windows Phone | About every 8 hours |
| Windows 8.1 | About every 8 hours |

If the device recently enrolled, the compliance, non-compliance, and configuration check-in runs more frequently, which is **estimated** at:

| Platform | Frequency |
| --- | --- |
| iOS/iPadOS | Every 15 minutes for 1 hour, and then around every 8 hours |  
| macOS | Every 15 minutes for 1 hour, and then around every 8 hours | 
| Android | Every 3 minutes for 15 minutes, then every 15 minutes for 2 hours, and then around every 8 hours | 
| Windows 10 PCs enrolled as devices | Every 3 minutes for 15 minutes, then every 15 minutes for 2 hours, and then around every 8 hours | 
| Windows Phone | Every 5 minutes for 15 minutes, then every 15 minutes for 2 hours, and then around every 8 hours | 
| Windows 8.1 | Every 5 minutes for 15 minutes, then every 15 minutes for 2 hours, and then around every 8 hours | 

At any time, users can open the Company Portal app, **Settings** > **Sync** to immediately check for policy or profile updates.

## What actions cause Intune to immediately send a notification to a device?

There are different actions that trigger a notification, such as when a policy, profile, or app is assigned (or unassigned), updated, deleted, and so on. These action times vary between platforms.

Devices check in with Intune when they receive a notification to check in, or during the scheduled check-in. When you target a device or user with an action, such as lock, passcode reset, app, profile or policy assignment, then Intune immediately notifies the device to check in to receive these updates.

Other changes, such as revising the contact information in the Company Portal app, don't cause an immediate notification to devices.

The settings in the policy or profile are applied at every check-in. The [Windows 10 MDM policy refresh blog post](https://www.petervanderwoude.nl/post/windows-10-mdm-policy-refresh/) may be a good resource.

## If multiple policies are assigned to the same user or device, how do I know which settings gets applied?

When two or more policies are assigned to the same user or device, then the setting that applies happens at the individual setting level:

- Compliance policy settings always have precedence over configuration profile settings.

- If a compliance policy evaluates against the same setting in another compliance policy, then the most restrictive compliance policy setting applies.

- If a configuration policy setting conflicts with a setting in another configuration policy, this conflict is shown in Intune. Manually resolve these conflicts.

## What happens when app protection policies conflict with each other? Which one is applied to the app?

Conflict values are the most restrictive settings available in an app protection policy *except* for the number entry fields, such as PIN attempts before reset. The number entry fields are set the same as the values, as if you created a MAM policy using the recommended settings option.

Conflicts happen when two profile settings are the same. For example, you configured two MAM policies that are identical except for the copy/paste setting. In this scenario, the copy/paste setting is set to the most restrictive value, but the rest of the settings are applied as configured.

A policy is deployed to the app and takes effect. A second policy is deployed. In this scenario, the first policy takes precedence, and stays applied. The second policy shows a conflict. If both are applied at the same time, meaning that there isn't preceding policy, then both are in conflict. Any conflicting settings are set to the most restrictive values.

## What happens when iOS/iPadOS custom policies conflict?

Intune doesn't evaluate the payload of Apple Configuration files or a custom Open Mobile Alliance Uniform Resource Identifier (OMA-URI) policy. It merely serves as the delivery mechanism.

When you assign a custom policy, confirm that the configured settings don't conflict with compliance, configuration, or other custom policies. If a custom policy and its settings conflict, then the settings are applied randomly.

## What happens when a profile is deleted or no longer applicable?

When you delete a profile, or you remove a device from a group that has the profile, then the profile and settings are removed from the device as described:

- Wi-Fi, VPN, certificate, and email profiles: These profiles are removed from all supported enrolled devices.
- All other profile types:  

  - **Windows and Android devices**: Settings aren't removed from the device
  - **Windows Phone 8.1 devices**: The following settings are removed:  
  
    - Require a password to unlock mobile devices
    - Allow simple passwords
    - Minimum password length
    - Required password type
    - Password expiration (days)
    - Remember password history
    - Number of repeated sign-in failures to allow before the device is wiped
    - Minutes of inactivity before password is required
    - Required password type – minimum number of character sets
    - Allow camera
    - Require encryption on mobile device
    - Allow removable storage
    - Allow web browser
    - Allow application store
    - Allow screen capture
    - Allow geolocation
    - Allow Microsoft account
    - Allow copy and paste
    - Allow Wi-Fi tethering
    - Allow automatic connection to free Wi-Fi hotspots
    - Allow Wi-Fi hotspot reporting
    - Allow wipe
    - Allow Bluetooth
    - Allow NFC
    - Allow Wi-Fi

  - **iOS/iPadOS**: All settings are removed, except:
  
    - Allow voice roaming
    - Allow data roaming
    - Allow automatic synchronization while roaming

## I changed a device restriction profile, but the changes haven't taken effect

Once set, Windows Phone devices don't allow security policies set using MDM or EAS to be reduced in security. For example, you set a **Minimum number of character password** to 8. You try to reduce it to 4. The more restrictive profile is already applied to the device.

To change the profile to a less secure value, then reset security policies. For example, in Windows 8.1, on the desktop, swipe in from right > select **Settings** > **Control Panel**. Select the **User Accounts** applet. In the left-hand navigation menu, there's a **Reset Security Policies** link (toward the bottom). Select it, and then choose **Reset Policies**.

Other MDM devices, such as Android, Windows Phone 8.1 and later, iOS/iPadOS, and Windows 10 may need to be retired, and re-enrolled in to Intune to apply a less restrictive profile.

## Some settings in a Windows 10 profile return "Not Applicable"

Some settings on Windows 10 devices may show as "Not Applicable". When this happens, that specific setting isn't supported on the version or edition of Windows running on the device. This message can occur for the following reasons:

- The setting is only available for newer versions of Windows, and not the current operating system (OS) version on the device.
- The setting is only available for specific Windows editions or specific SKUs, such as Home, Professional, Enterprise, and Education.

To learn more about the version and SKU requirements for the different settings, see the [Configuration Service Provider (CSP) reference](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference).

## Next steps

Need extra help? See [How to get support for Microsoft Intune](../fundamentals/get-support.md).
