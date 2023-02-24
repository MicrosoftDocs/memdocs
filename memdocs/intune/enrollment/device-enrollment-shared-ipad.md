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
ms.collection:
- tier2
- M365-identity-device-management
---

# Shared iPad devices  
*Applies to iPadOS 13.4 and later*    

Provisioning a device as a Shared iPad sets it up so that it can be shared among more than one employee or student. iPads enrolled in Intune using automated device enrollment, and without user affinity, can be provisioned as shared iPads. 

A Shared iPad consists of a pre-defined number of *user partitions*. User partitions ensure that each user’s apps, data, and preferences are stored separately on the iPad. If you allow it, these partitions can be backed up to iCloud for seamless transition across other shared iPads in your organization. 

When you federate your organization’s Azure AD instance in Apple Business or School Manager, a device user can sign in on a Shared iPad using their Azure AD username and password. This automatically creates a Managed Apple ID for the user that matches their Azure AD username when they sign in on a Shared iPad for the first time. In addition, at first sign-in on a Shared iPad, the user sets up an alphanumeric passcode for their user partition and the apps assigned to the device are installed to the user partition. The next time the user accesses a Shared iPad, they only need to provide their Managed Apple ID (same as their Azure AD username) and the alphanumeric passcode. 

## Configure Shared iPad

Follow these steps to set up Shared iPad in your environment.  

>[!IMPORTANT]
> Shared iPad is supported on supervised iPads running iPadOS 13.3 and later. A device wipe will be required if an enrollment profile enabled with Shared iPad is sent to a device that doesn't support Shared iPad. Shared iPad isn't supported on iPhones, or iPads running iOS/iPadOS version 13.3 and earlier. 

1. Federate your Azure AD instance with Apple Business Manager or Apple School Manager. For more information, see [Intro to federated authentication with Apple Business Manager](https://support.apple.com/guide/apple-business-manager/intro-to-federated-authentication-apdb19317543/web).
2. Create an enrollment profile.  
    1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
    2. Go to **Devices** > **iOS/iPadOS** > **iOS/iPadOS Enrollment**.
    2. Select **Enrollment program tokens**.
    4. Choose a token, and then select  **Profiles** > **Create profile** > **iOS/iPadOS**. 
3. Configure these settings in the enrollment profile: 
     1. Go to **Management settings** and enable **Shared iPad**.  
     2. Set **User affinity** to **Enroll without user affinity**.  
     3. Set **Supervised** to **Yes**.  
     4. Set **Shared iPad** to **Yes**. 
4. Select **Save** when you're done configuring the rest of your profile.
5. Assign devices synced from Apple Business Manager. 
    1. Select the new enrollment profile.  
    2. Select **Assign devices** > **Add devices**.  
6. Create a dynamic device group to automatically assign this profile to devices that fall within your rule parameters. 
    1. Go to **Groups** > **New group**. 
    1. For **Membership type**, select **Dynamic Device**. 
    2. Select **Add dynamic query**.
    4. In the **Property** column, select  **enrollmentProfileName**. 
    5. In the **Value** column, enter the name of your enrollment profile.  
7. Assign all required apps and configuration profiles to the dynamic device group.  
8. Prepare new and existing devices for deployment:  
   * Turn on new devices and follow the onscreen prompts to set up Shared iPad. 
   * Reset existing devices to factory settings and follow the onscreen prompts to set up Shared iPad.  

## Configure settings for Shared iPads  

> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

You can configure Shared iPad settings in a device configuration profile for both device and user context. In general:

* Device-applicable settings apply to any active user on a Shared iPad device.
* User-applicable settings apply when the user is active on any Shared iPad device.  

The following table describes the applicability rules for Shared iPad settings.  

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

### You should know  
When creating the device configuration profile for Shared iPads, keep in mind that:  

- Your Azure AD instance must be federated in Apple Business Manager for a user group policy assignment to succeed.  
- All device configuration profile settings are device applicable for Shared iPad temporary sessions.  
- User-assigned policies apply to a shared iPad when the user signs in using their federated Azure AD credentials. For more information about federating an Azure AD instance with Apple Business Manager, see the [Apple Business Manager guide](https://support.apple.com/guide/apple-business-manager-m/apdb19317543/web) (opens Apple support website).  
- Device-assigned policies apply to a shared iPad when you initiate a device-sync from the admin center, or when Intune notifies the device to check in with the Intune service. For more information about frequency of device check-ins, see [How long does it take for devices to get a policy, profile, or app after they are assigned?](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)   


## Configure temporary sessions 

  In iPadOS 13.4 or later, users can initiate a temporary session by tapping **Guest** on the device sign-in screen. A *temporary session* allows users to sign in to the device as a guest, and doesn't require them to enter a Managed Apple ID or password. All user data, including browsing history, is deleted when the user signs out of the session. Temporary sessions are allowed by default with Shared iPad. For more information, see [Shared iPad overview](https://support.apple.com/guide/deployment/dep9a34c2ba2/1/web/1.0) (opens Apple documentation).   
 
 You can configure temporary sessions in an iOS device restrictions profile in the admin center. For more information, see [Shared iPad - Automated device enrollment (supervised)](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised-10). 

## Add apps 

You can deploy volume-purchased (VPP), apps, custom apps, line-of-business apps, or web apps to a Shared iPad device.  

* To add a VPP or custom app in the admin center, add the apps in Apple Business Manager or Apple School Manager and sync the VPP token with Intune. Assign a VPP or custom app as device-licensed to Azure AD device groups in Intune. For more information, see [Sync a VPP token](../apps/vpp-apps-ios.md#synchronize-a-vpp-token).
* Add a line-of-business app in the admin center and assign it to Azure AD device groups. For more information, see [Add an iOS/iPadOS line-of-business app to Microsoft Intune](../apps/lob-apps-ios.md).
* Add a web app, also referred to as a *web clip*, in the admin center and assign it to Azure AD user groups. For more information, see [Add a web app to Intune](../apps/web-app.md#add-a-web-app-to-intune).   

The following table shows each iOS app type and describes the type of assignment supported with shared iPads.  

|     App type    |     Applicability on device group assignment    |     Applicability on user group assignment    |
|---|---|---|
|     Line-of-business app    |     Device    |     Not applicable    |
|     Device-licensed volume-purchased or custom app (VPP)    |     Device    |     Not applicable    |
|     User-licensed volume-purchased or custom app (VPP)    |     Not applicable    |     Not applicable    |
|     Web app    |     Not supported    |     User    |
|     App Store app    |     Not applicable    |     Not applicable    |  

Configure home screen layout settings in a device configuration profile to organize the app layout and folders on the home screen and dock. Assign the profile to Azure AD user groups. For more information, see [Home screen layout](../configuration/ios-device-features-settings.md#home-screen-layout).  

## Recommended policy and app assignment for Shared iPads

The following table describes various deployment scenarios and our recommendations for configurations. Use the table as reference when planning Shared iPad deployment and configuration in your environment.  

| Scenario | Admin configuration | Shared iPad experience | Example |
|---|---|---|---|
| All   users on a Shared iPad are in the same role. <p><p> All users on   a Shared iPad are using temporary sessions. | Assign   all apps and profiles to Azure AD device group containing Shared iPads. | All   apps and profiles apply to any active user on the Shared iPad or to Shared   iPad temporary sessions. | You   assign a Wi-Fi profile, device restrictions, VPP apps and home screen layout   to an Azure AD device group containing a Shared iPad. These profiles apply to   any user signing in on the Shared iPad. |
| Users   on a Shared iPad are in different roles. | <ul><li>Assign all apps   and profiles common to all roles to an Azure AD device group containing   Shared iPads.</li><li>Assign profiles that vary by role and are   user applicable to user groups. Ensure that the profile does not conflict   with any setting assigned to the device group above.</li></ul> | When a user signs in on a Shared   iPad, the combination of device-targeted profiles and user-targeted profiles   creates a customized experience for the active user.<p><p>Only   apps and profiles assigned to the device apply to Shared iPad temporary   sessions.  | You assign a   common Wi-Fi profile and all VPP apps to a device group containing a Shared   iPad. Then you assign varying home screen layouts to different roles using   Azure AD user groups. This customizes the Shared iPad experience for users in   each role. |
| Apply   different device restrictions to different users on a Shared iPad. | <ul><li>Assign device   restrictions that should apply to all users of the Shared iPad to an Azure   device group containing the Shared iPads.</li><li>Assign   user-applicable device restrictions that vary by user to Azure AD user groups.   Ensure that the device restrictions do not conflict with any device   restrictions assigned to the device group.</li></ul> | When a user signs in on a Shared   iPad, the combination of device targeted restrictions and user-targeted   restrictions creates a customized experience for the active   user.<p><p>Only device restrictions assigned to device groups   apply to Shared iPad temporary sessions. | You want to prevent all Shared   iPad users from using AirDrop. But you only want managers to be able to turn   off Wi-Fi on Shared iPads.<p><p>You assign a device configuration   profile that blocks AirDrop to a device group containing a Shared iPad. Then   you assign a device configuration profile that requires Wi-Fi to be always on   to a user group containing non-manager employees. |
| Show/hide   different apps to different users on a Shared iPad. | <ul><li>Assign all apps to the Azure AD device group containing Shared iPads.</li><li>Create   home screen layouts to show/hide the apps and assign the home screen layouts to Azure AD user groups.</li></ul> | When a user signs in on a Shared iPad, the user-assigned home screen layout applies to show/hide the apps as configured in Microsoft Intune.<p><p>All apps assigned to the device show in Shared iPad temporary sessions. | You assign   Microsoft Outlook, Microsoft Teams, and Safari to a device group containing a Shared   iPad. Then you assign a home screen layout that only shows Teams to a user group containing users who only require Teams when using Shared iPad. You assign another home screen layout that shows Outlook, Teams and Safari to a user group containing managers who need access to all three apps when using Shared iPad. |
| Hide unnecessary system apps on a Shared iPad. | Create a home screen layout containing the desired system apps and managed apps. Assign the home screen layout to the Azure AD device group containing Shared iPads. | The same home screen layout will apply to any user signing in on the Shared iPad and to Shared iPad temporary sessions. | You create a home screen layout that excludes unnecessary system apps like Settings, App Store, Clock and assign the layout to a device group containing a Shared iPad. 

We recommend that you configure a setting only once for Shared iPad. Don't configure multiple values of a setting for a Shared iPad. If multiple values of a setting are configured, the setting that applies can't be pre-determined. If Intune does detect the conflict, it will apply the first setting assigned to the device. If a setting that is both device applicable and user applicable is assigned to an Azure AD device group and an Azure AD user group, the applied value of the setting is chosen by the operating system.  

## Known limitations

The following limitations exist in Intune for Shared iPad:  

- Disabled settings and system apps: A limited number of settings and system apps are available with Shared iPad. For more information about unavailable settings and apps, see [Use Shared iPad with Managed Apple IDs](https://support.apple.com/guide/apple-business-manager/axm3a8bb0ab8/web).  
- App Store installations disabled: The App Store is available by default with Shared iPad, but app installation is disabled so users can't install apps from the App Store. We recommended disabling the App Store in an Intune configuration profile to avoid confusion with users.  
- Company Portal and available apps not supported: Intune Company Portal app and the Intune Company Portal website are not supported with Shared iPad.
- App assignment requirements: You must assign apps as _required_ to device groups. *Available* apps are not supported with Shared iPad.  
- Passcode complexity can't be managed with Shared iPad: Shared iPad passcodes must have eight alphanumeric characters, and can't be changed in Apple Business Manager. The passcode complexity and length settings available in Intune device configuration profiles don't apply to Shared iPad. An MDM administrator can set the grace period, which specifies the number of minutes a user has to unlock the iPad without a passcode.  
- Some policies not supported: These Intune policies are not supported with Shared iPad: app-based and device-based conditional access policies, app protection policies, and compliance policies. 
- Wallpaper not supported: Wallpapers aren't supported on Shared iPad devices. 
- Email profile not supported: Email profiles aren't supported with Shared iPad. An error occurs when you assign an email profile to a Shared iPad device.  
- User-assigned policies don't appear in reports: Intune doesn't report device status or user status in reports for Shared iPad apps and profiles assigned to Azure AD user groups.  
- Azure AD federation requirement not enforced: The Azure AD federation requirement isn't enforced. If the Managed Apple ID matches the Azure AD UPN, and the Azure AD user is assigned a user applicable device configuration profile, the profile will apply to the user when they sign in to a shared iPad using their Managed Apple ID.  

## Next steps

- [Set up iOS/iPadOS device enrollment with Apple Configurator](../enrollment/apple-configurator-enroll-ios.md)
