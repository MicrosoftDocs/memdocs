---
# required metadata

title: Shared iPad devices
titleSuffix: Microsoft Intune
description: Learn about Shared iPad devices.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/08/2021
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

#ms.reviewer:
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
3. Enable **Shared iPad** in the enrollment profile under **Management settings**. Set **User affinity** to **Enroll without user affinity** and **Shared iPad** to **Yes**. Important note - A device wipe will be required if an iOS/iPadOS enrollment profile with Shared iPad enabled is sent to an unsupported device. Unsupported devices include any iPhone models, and iPads running iPadOS/iOS 13.3 and earlier. Supported devices include iPads running iPadOS 13.3 and later. 
4. Complete configuring the enrollment profile as desired and then select **Save**.
5. Assign devices synced from Apple Business Manager by selecting the new enrollment profile, then select **Assign devices** > **Add devices**.
6. Create a dynamic device group containing devices by using the new enrollment profile for Shared iPad by navigating to **Groups** > **New group**. Set **Membership type** to **dynamic device** and select **Add dynamic query** and set **enrollmentProfileName** to the *name of desired enrollment profile*.
7. Assign required apps and configuration profiles for Shared iPads to the dynamic device group.
8. For new devices, power on and follow the prompts to set up the device as a Shared iPad. For existing devices, factory reset the device and follow the prompts to set it up as a Shared iPad.

## Configure temporary sessions on Shared iPads

In iPadOS 13.4 or later, users can initiate a [temporary session](https://support.apple.com/guide/mdm/mdm6c592d817/web) without the need for a username or password by tapping Guest at the login screen. All their data — including browsing history — is deleted when the user signs out. Temporary sessions allow users to sign in as Guest, and users are not required to enter a Managed Apple ID or password. This can be configured using iOS Device Restrictions in Endpoint Manager. For more information, see [Shared iPad - Automated device enrollment (supervised)](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised-10) as mentioned in this document. Temporary sessions are allowed by default on Shared iPads.

## Add Apps on Shared iPads

You can deploy volume-purchased (VPP) apps or custom apps or web apps to Shared iPads. 
1. To deploy a VPP or custom app to Endpoint Manager, add the apps in Apple Business Manager or Apple School Manager and synchronize the VPP token and assign it in Intune. For more information, see [Synchronize a VPP token](../apps/vpp-apps-ios.md#synchronize-a-vpp-token).
2. To add a line-of-business app in Endpoint Manager and assign it to Azure AD group. For more information, see [Add an iOS/iPadOS line-of-business app to Microsoft Intune](../apps/lob-apps-ios.md).
3. To add a web app in Endpoint Manager and assign it to Azure AD groups. For more information, see [Add a web app to Intune](../apps/web-app.md#add-a-web-app-to-intune). 
4. For assigning apps to shared iPads, you should use Azure AD device groups. Using Azure AD user groups for assignment to Shared iPads is currently not supported. 

> [!NOTE]
> One of the ways to create Azure AD device group is to use [Azure AD dynamic device group](/azure/active-directory/enterprise-users/groups-dynamic-membership#rules-for-devices) and create it based on the enrollmentProfileName. This is the name of the enrollment profile as per steps mentioned above for configuring shared iPads.

## Known limitations

The following are known limitation when working with shared iPads:

- **Disabled settings and system apps:** Shared iPads provide users access to a limited number of settings and system apps. For more information on what settings and apps are disabled on Shared iPads. For more information, see [Shared iPad and Managed Apple IDs](https://support.apple.com/guide/mdm/shared-ipad-and-managed-apple-ids-mdm9992c9a34/web).
- **User group assignment is not supported:** Microsoft Intune currently only supports device-assigned policies and apps on Shared iPads. User-assigned apps and policies will not apply on Shared iPads.
- **App Store installations are disabled:** The App Store is available by default on Shared iPad. But app installation is disabled for App Store apps when a device is set up as a Shared iPad. It is recommended that you disable App Store using configuration profiles in Intune.
- **Company Portal and available apps are not supported:** Intune Company Portal app and the Intune Company Portal website are not supported on Shared iPads. Apps must be assigned as “required” to device groups containing the Shared iPad to install. Available apps are currently not supported on Shared iPad.
- **Passcode complexity cannot be managed on Shared iPad:** The passcode complexity for Shared iPad is a complex 8 character alphanumeric and cannot be changed in Apple Business Manager. The passcode complexity and length settings available in device configuration profile do not apply to Shared iPads. The MDM administrator can set the grace period – a number of minutes during which the user can unlock the iPad without a passcode.
- **Unsupported scenarios:** Some Intune scenarios are not supported on Shared iPads, namely, app-based and device-based Conditional Access, app protection policies and compliance policies.
- **Wallpaper is not supported:** Setting a wallpaper image is currently not supported on Shared iPad. For more information on wallpaper, see [iOS/iPadOS Device Features](https://docs.microsoft.com/mem/intune/configuration/ios-device-features-settings#wallpaper). 


## Next steps

- [Set up iOS/iPadOS device enrollment with Apple Configurator](../enrollment/apple-configurator-enroll-ios.md)
