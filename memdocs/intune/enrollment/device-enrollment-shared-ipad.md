---
# required metadata

title: Shared iPad devices
titleSuffix: Microsoft Intune
description: Learn about Shared iPad devices.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/13/2021
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: M365-identity-device-management
---

# Shared iPad devices

Provisioning a device as a Shared iPad sets it up for use by multiple users. iPads running on iPadOS 13.4 and later can be provisioned as a Shared iPad when enrolled using Automated Device Enrollment without user affinity. 

A Shared iPad consists of a pre-defined number of user partitions. User partitions ensure that each user’s apps, data, and preferences are stored separately on Shared iPad and can be backed up to iCloud (if allowed by admin) for seamless transition across multiple Shared iPads. 

By federating your organization’s AAD instance in Apple Business or School Manager, a user can sign in on a Shared iPad using their AAD username and password. This automatically creates a Managed Apple ID for the user that matches their AAD username when they sign in on a Shared iPad for the first time. In addition, at first sign-in on a Shared iPad, the user sets up an alphanumeric passcode for their user partition and the apps assigned to the device are installed to the user partition. The next time the user accesses a Shared iPad, they only need to provide their Managed Apple ID (same as their AAD username) and the alphanumeric passcode. 

## Configure Shared iPad

Follow these steps to set up Shared iPads in your environment:
1. Federate your AAD instance with Apple Business Manager or Apple School Manager. For more information, see [Intro to federated authentication with Apple Business Manager](https://support.apple.com/guide/apple-business-manager/intro-to-federated-authentication-apdb19317543/web).
2. Create an enrollment profile by navigating to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and selecting **Devices** > **iOS/iPadOS** > **iOS/iPadOS Enrollment** > **Enrollment program tokens* > *select a token* > **Profiles** > **Create profile** > **iOS/iPadOS**. 
3. Enable **Shared iPad** in the enrollment profile under **Management settings**. Set **User affinity** to **Enroll without user affinity** and **Supervised** to **Yes** and then **Shared iPad** to **Yes**. Important note - A device wipe will be required if an iOS/iPadOS enrollment profile with Shared iPad enabled is sent to an unsupported device. Unsupported devices include any iPhone models, and iPads running iPadOS/iOS 13.3 and earlier. Supported devices include iPads running iPadOS 13.3 and later. Shared iPads must be supervised.
4. Complete configuring the enrollment profile as desired and then select **Save**.
5. Assign devices synced from Apple Business Manager by selecting the new enrollment profile, then select **Assign devices** > **Add devices**.
6. Create a dynamic device group containing devices by using the new enrollment profile for Shared iPad by navigating to **Groups** > **New group**. Set **Membership type** to **dynamic device** and select **Add dynamic query** and set **enrollmentProfileName** to the *name of desired enrollment profile*.
7. Assign required apps and configuration profiles for Shared iPads to the dynamic device group.
8. For new devices, power on and follow the prompts to set up the device as a Shared iPad. For existing devices, factory reset the device and follow the prompts to set it up as a Shared iPad.

## Configure settings for Shared iPads

> [!NOTE]
> *This feature is in public preview.*

You can configure settings in device configuration profiles for a Shared iPad both in device and user context. However, the settings on a Shared iPad follow the applicability rules in the table below. In general, a device applicable setting applies to any active user on a Shared iPad device, while a user applicable setting applies when the user is active on any Shared iPad device.

> [!NOTE]
> - Your Azure AD instance must be federated in Apple Business Manager for user group policy assignment to succeed.
> - All device configuration profile settings are device applicable for Shared iPad temporary sessions.
> - User-assigned policies apply to a Shared iPad when the user signs in using their federated Azure AD credentials. See [Apple’s documentation](https://support.apple.com/guide/apple-business-manager-m/apdb19317543/web) on federating an Azure AD instance with Apple Business Manager.
> - Device-assigned policies apply to a Shared iPad when you initiate a device-sync from MEM admin console or when Intune notifies the device to check in with the Intune service. [Learn more about frequency of device check-in with the Intune service](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

| Profile   type | Setting name | Applicability on device group   assignment | Applicability on user group   assignment |
|---|---|---|---|
| Device features | Home screen layout | Device | User |
| Device features | App notifications | Device | User |
| Device features | Single sign on app extension | Device | User |
| Device features | AirPrint settings | Device | Not applicable |
| Device features | Lock screen message | Device | Not applicable |
| Device features | Web content filter | Device | Not applicable |
| Device restrictions | Block Shared iPad temporary   sessions | Device | Not applicable |
| Device restrictions | Defer software updates | Device | Not applicable |
| Device restrictions | Force automatic date and time | Device | Not applicable |
| Device restrictions | Require joining Wi-Fi networks   only using configuration profiles | Device | Not applicable |
| Device restrictions | Block auto lock | Device | Not applicable |
| Device restrictions | Allow users to boot devices into   recovery mode with unpaired devices | Device | Not applicable |
| Device restrictions | Block Siri for dictation | Device | Not applicable |
| Device restrictions | All other settings in device   restrictions | Device | User |
| Email | All settings | Device | User |
| VPN, Wi-Fi, Certificate | All settings | Device | Not applicable |

## Configure temporary sessions on Shared iPads

In iPadOS 13.4 or later, users can initiate a [temporary session](https://support.apple.com/guide/mdm/mdm6c592d817/web) without the need for a username or password by tapping Guest at the login screen. All their data — including browsing history — is deleted when the user signs out. Temporary sessions allow users to sign in as Guest, and users are not required to enter a Managed Apple ID or password. This can be configured using iOS Device Restrictions in Endpoint Manager. For more information, see [Shared iPad - Automated device enrollment (supervised)](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised-10) as mentioned in this document. Temporary sessions are allowed by default on Shared iPads.

## Add Apps on Shared iPads

You can deploy volume-purchased (VPP) apps or custom apps or line-of-business apps or web apps to Shared iPads.

1. To deploy a VPP or custom app to Endpoint Manager, add the apps in Apple Business Manager or Apple School Manager and synchronize the VPP token. Assign a VPP or custom app as device-licensed to Azure AD device groups in Intune. For more information, see [Synchronize a VPP token](../apps/vpp-apps-ios.md#synchronize-a-vpp-token).
2. To add a line-of-business app in Endpoint Manager and assign it to Azure AD device group. For more information, see [Add an iOS/iPadOS line-of-business app to Microsoft Intune](../apps/lob-apps-ios.md).
3. To add a web app in Endpoint Manager and assign it to Azure AD groups. For more information, see [Add a web app to Intune](../apps/web-app.md#add-a-web-app-to-intune). 
4. For assigning apps to Shared iPads, you should use Azure AD device groups. You can use home screen layout settings in device configuration profile assigned to Azure AD user groups to show or hide different sets of apps to different users on a Shared iPad.  

App installations on Shared iPads follow the applicability rules in the table below.<p>

|     App type    |     Applicability on device group assignment    |     Applicability on user group assignment    |
|---|---|---|
|     Line-of-business app    |     Device    |     Not applicable    |
|     Device-licensed volume-purchased or custom app (VPP)    |     Device    |     Not applicable    |
|     User-licensed volume-purchased or custom app (VPP)    |     Not applicable    |     Not applicable    |
|     Web app    |     Device    |     User    |
|     App Store app    |     Not applicable    |     Not applicable    |

## Recommended policy and app assignment for Shared iPads

You should review the scenarios and recommendations in the table below when planning Shared iPad deployment and configuration in your environment. 

| Scenario | Admin configuration | Shared iPad experience | Example |
|---|---|---|---|
| All   users on a Shared iPad are in the same role. <p><p> All users on   a Shared iPad are using temporary sessions. | Assign   all apps and profiles to Azure AD device group containing Shared iPads. | All   apps and profiles apply to any active user on the Shared iPad or to Shared   iPad temporary sessions. | You   assign a Wi-Fi profile, device restrictions, VPP apps and home screen layout   to an Azure AD device group containing a Shared iPad. These profiles apply to   any user signing in on the Shared iPad. |
| Users   on a Shared iPad are in different roles. | <ul><li>Assign all apps   and profiles common to all roles to an Azure AD device group containing   Shared iPads.</li><li>Assign profiles that vary by role and are   user applicable to user groups. Ensure that the profile does not conflict   with any setting assigned to the device group above.</li></ul> | When a user signs in on a Shared   iPad, the combination of device-targeted profiles and user-targeted profiles   creates a customized experience for the active user.<p><p>Only   apps and profiles assigned to the device apply to Shared iPad temporary   sessions.  | You assign a   common Wi-Fi profile and all VPP apps to a device group containing a Shared   iPad. Then you assign varying home screen layouts to different roles using   Azure AD user groups. This customizes the Shared iPad experience for users in   each role. |
| Apply   different device restrictions to different users on a Shared iPad. | <ul><li>Assign device   restrictions that should apply to all users of the Shared iPad to an Azure   device group containing the Shared iPads.</li><li>Assign   user-applicable device restrictions that vary by user to Azure AD user groups.   Ensure that the device restrictions do not conflict with any device   restrictions assigned to the device group.</li></ul> | When a user signs in on a Shared   iPad, the combination of device targeted restrictions and user-targeted   restrictions creates a customized experience for the active   user.<p><p>Only device restrictions assigned to device groups   apply to Shared iPad temporary sessions. | You want to prevent all Shared   iPad users from using AirDrop. But you only want managers to be able to turn   off Wi-Fi on Shared iPads.<p><p>You assign a device configuration   profile that blocks AirDrop to a device group containing a Shared iPad. Then   you assign a device configuration profile that requires Wi-Fi to be always on   to a user group containing non-manager employees. |
| Show/hide   different apps to different users on a Shared iPad. | <ul><li>Assign all apps to   the Azure AD device group containing Shared iPads.</li><li>Create   home screen layouts to show/hide the apps and assign the home screen layouts   to Azure AD user groups.</li></ul> | When a user signs in on a Shared   iPad, the user-assigned home screen layout applies to show/hide the apps as   configured in Microsoft Endpoint Manager.<p><p>All apps assigned   to the device show in Shared iPad temporary sessions. | You assign   Microsoft Outlook, Teams and Safari to a device group containing a Shared   iPad. Then you assign a home screen layout that only shows Teams to a user   group containing users who only require Teams when using Shared iPad. You   assign another home screen layout that shows Outlook, Teams and Safari to a   user group containing managers who need access to all 3 apps when using   Shared iPad. |
| Hide   unnecessary system apps on a Shared iPad. | Create a home screen layout   containing the desired system apps and managed apps. Assign the home screen   layout to the Azure AD device group containing Shared iPads. | The same home screen layout will   apply to any user signing in on the Shared iPad and to Shared iPad temporary   sessions. | You create a home screen layout   that excludes unnecessary system apps like Settings, App Store, Clock and   assign the layout to a device group containing a Shared iPad. |

> [!NOTE]
> - It is recommended that a setting is configured only once for Shared iPads. 
> - Configuring multiple values of a setting for a Shared iPad is not recommended. If multiple values of a setting are configured, the setting that applies cannot be pre-determined. 
>   - Intune may detect the conflict and the first setting assigned to the device would apply.
>   - If a setting that is both device applicable and user applicable is assigned to an Azure AD device group and an Azure AD user group, the applied value of the setting is chosen by iPadOS.

## Known limitations

The following are known limitations when working with shared iPads:

- **Disabled settings and system apps:** Shared iPads provide users access to a limited number of settings and system apps. For more information on what settings and apps are disabled on Shared iPads. For more information, see [Shared iPad and Managed Apple IDs](https://support.apple.com/guide/mdm/shared-ipad-and-managed-apple-ids-mdm9992c9a34/web).
- **App Store installations are disabled:** The App Store is available by default on Shared iPad. But app installation is disabled for App Store apps when a device is set up as a Shared iPad. It is recommended that you disable App Store using configuration profiles in Intune.
- **Company Portal and available apps are not supported:** Intune Company Portal app, the Intune Company Portal website are not supported on Shared iPads. Apps must be assigned as “required” to device groups containing the Shared iPad to install. Available apps are supported on Shared iPad.
- **Passcode complexity cannot be managed on Shared iPad:** The passcode complexity for Shared iPad is a complex 8 character alphanumeric and cannot be changed in Apple Business Manager. The passcode complexity and length settings available in device configuration profile do not apply to Shared iPads. The MDM administrator can set the grace period – a number of minutes during which the user can unlock the iPad without a passcode.
- **Unsupported scenarios:** Some Intune scenarios are not supported on Shared iPads, namely, app-based and device-based Conditional Access, app protection policies and compliance policies.
- **Wallpaper is not supported:** Setting a wallpaper image is currently not supported on Shared iPad. For more information on wallpaper, see [iOS/iPadOS Device Features](../configuration/ios-device-features-settings.md#wallpaper). 
- Email profile shows error: if you assign an email profile to Shared iPads, it reports error. Email profiles on Shared iPad are currently not supported.
- User-assigned policies applying to Shared iPads do not show in reports: apps and profiles assigned to Azure AD user groups do not reflect status in “device status” and “user status” under Monitoring section of the apps or profiles when they apply on Shared iPads.
- Azure AD federation requirement is not enforced: if the Managed Apple ID matches the Azure AD UPN and the Azure AD user is assigned a user applicable device configuration profile, the profile will apply to the user when they sign in using their Managed Apple ID on a Shared iPad. The Azure AD federation requirement is currently not enforced.

## Next steps

- [Set up iOS/iPadOS device enrollment with Apple Configurator](../enrollment/apple-configurator-enroll-ios.md)
