---
title: Set up automated device enrollment (ADE) for visionOS
description: Learn how to enroll corporate-owned Apple Vision Pro devices into Microsoft Intune with Apple Automated Device Enrollment (ADE).
ms.date: 04/21/2026
ms.topic: how-to
ms.reviewer: annovich
ai-usage: ai-assisted
ms.collection:
- M365-identity-device-management
---

# Set up automated device enrollment for visionOS

*Applies to visionOS*

This article describes how to create a visionOS enrollment policy for Apple automated device enrollment (ADE) in Microsoft Intune. This type of enrollment profile is for devices without user affinity. For an overview of ADE and prerequisite setup, see [Overview of Apple Automated Device Enrollment](overview-automated-enrollment-apple.md).

## Prerequisites
Before you create the enrollment profile, you must have:

* Access to [Apple Business portal](https://business.apple.com/) or [Apple School Manager portal](https://school.apple.com/).
* An active Apple token (.p7m file). For steps, see [Set up an ADE token](setup-apple-token.md).
* An [Apple MDM push certificate in Intune](create-mdm-push-certificate.md).
* New or wiped Apple Vision Pro devices purchased from Apple Business or Apple School Manager.
     > [!Tip]
     > Automated device enrollment applies device configurations that a device user may not be able to remove. Wipe all devices prior to enrollment to return them to an out-of-box state.

## Deploy the Company Portal app

When using automated device enrollment (ADE), deploy the Intune Company Portal app through Intune — not through the App Store. Deploying through Intune is the only way to:

- Ensure all ADE devices, including already-enrolled ones, receive the app.
- Enable automatic app updates for the Company Portal on ADE devices.

> [!IMPORTANT]
> Don't use the App Store version of the Company Portal app. It isn't compatible with automated device enrollment and doesn't provide the automatic updates and availability that deployment does.

### Deploy Company Portal as a VPP app

Deploy the app as a required VPP app [with device licensing](../../intune-service/apps/vpp-apps-ios.md#how-are-purchased-apps-licensed). For information about how to sync, assign, and manage a VPP app, see [Assign a volume-purchased app](../../intune-service/apps/vpp-apps-ios.md#assign-a-volume-purchased-app).

To enable automatic app updates for Company Portal, go to your app token settings in the admin center and change **Automatic app updates** to **Yes**. See [Upload an Apple VPP or Apple Business location token](../../intune-service/apps/vpp-apps-ios.md#upload-an-apple-vpp-or-apple-business-manager-location-token) for the steps to access your token settings. If you don't enable automatic updates, the device user must manually check for them.

## Create an enrollment profile

Create a visionOS enrollment profile for userless automated device enrollment. A device enrollment profile defines the settings applied to a group of devices during enrollment. There's a limit of 1,000 enrollment profiles per enrollment token.

> [!NOTE]
> Devices are blocked from enrolling when there aren't enough Company Portal licenses for a VPP token or if the token expires. Intune alerts you when a token is about to expire or licenses are running low.

1. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices**.
1. Expand **Device onboarding**, and then select **Enrollment**.
1. Select the **Apple mobile** tab.
1. Choose **Enrollment program tokens**.
1. Choose a token, and then select **Profiles**.
1. Select **Create profile** > **visionOS**.
1. For **Basics**, give the profile a **Name** and **Description** for administrative purposes. Users don't see these details.
1. Select **Next**.

   > [!IMPORTANT]
   > You must assign an enrollment policy to your devices before the devices become active. We recommend that you set a default enrollment policy as soon as possible so that as devices sync from Apple Business or Apple School Manager, and then turn on, they can enroll correctly through automated device enrollment. If a device you synced from Apple isn't assigned an enrollment policy and someone turns it on to set it up, enrollment fails.

    > [!IMPORTANT]
    > If you make changes to an existing enrollment profile, the new settings won't take effect on assigned devices until devices are reset back to factory settings and reactivated. The device name template setting is the only setting you can change that doesn't require a factory reset to take effect. Changes to the naming template take effect at the next check-in.

1. If you want devices using this profile to be supervised, select **Yes** in the **Supervised** list.

    Supervised devices give you more management options and disabled Activation Lock by default. We recommend that you use ADE as the mechanism for enabling supervised mode, especially if you're deploying large numbers of visionOS devices.

1. In the **Locked enrollment** list, select **Yes** or **No**. Locked enrollment disables visionOS settings that allow the management profile to be removed. If you enable locked enrollment, users won't be able to unenroll their device.

    > [!IMPORTANT]
    > This setting is different from the remove and reset options in the Company Portal app. Regardless of how you configure locked enrollment, the **Remove Device** or **Factory Reset** options in the Company Portal app remain unavailable on devices enrolled through automated device enrollment. Users won't be able to remove the device on the Company Portal website either. For more information about the self-service actions available on enrolled devices, see [Self-service actions](../../app-management/configuration/configure-company-portal.md#self-service-actions).

1. In the **Sync with computers** list, select an option for the devices that use this profile. If you select **Allow Apple Configurator by certificate**, you need to choose a certificate (.cer extension) under **Apple Configurator Certificates**.

1. If you selected **Allow Apple Configurator by certificate** in the previous step, choose an Apple Configurator certificate (.cer extension) to import. The limit is 10 certificates.

1. For **Await final configuration**, your options are:
      * **Yes**: Enable a locked experience at the end of Setup Assistant to ensure your most critical device configuration policies are installed on the device. Just before the home screen loads, Setup Assistant pauses and lets Intune check in with the device. The end-user experience locks while users await final configurations.

         The amount of time that users are held on the Awaiting final configuration screen varies, and depends on the total number of policies and apps you apply to the device. The more policies and apps assigned to the device, the longer the waiting time. Setup Assistant and Microsoft Intune don't enforce a minimum or maximum time limit during this portion of setup.

           >[!NOTE]
           > Only device configuration policies start installing during the awaiting final configuration screen, and applications aren't included in this.

         This setting is applied once during the out-of-box automated device enrollment experience in Setup Assistant. The device user doesn't experience it again unless they re-enroll their device. **Yes** is the default setting for new enrollment profiles.

      * **No**: The device is released to the home screen when Setup Assistant ends, regardless of policy installation status. Device users might be able to access the home screen or change device settings before all policies are installed. **No** is the default setting for existing enrollment profiles.

1. Optionally, create a device name template to quickly identify devices assigned this profile in the admin center. Intune uses your template to create and format device names. The names are given to devices when they enroll and upon each successive check-in. To create a template:
 1. Under **Apply device name template**, select **Yes**.
 2. In the **Device Name Template** box, enter the template you want to use to construct device names. The template can include the device type and serial number. It can't contain more than 63 characters, including the variables. Example: `{{DEVICETYPE}}-{{SERIAL}}`

1. Select **Next**.

1. On the **Setup Assistant** tab, configure the following profile settings:

    | Department setting | Description |
    |---|---|
    | **Department** | Appears when users tap **About Configuration** during activation. |
    |    **Department Phone**     | Appears when users tap the **Need Help** button during activation. |

    For a description of all screens, see [Setup Assistant screen reference](#setup-assistant-screen-reference) (in this article).
    All screens are shown during setup but only if there are steps to complete after the restore or after the software update. Users can sometimes skip the screen without taking action. They can go to the device's **Settings** menu later to set up the feature.  

1. Select **Next**.

1. To save the profile, select **Create**.

<a name='dynamic-groups-in-azure-active-directory'></a>

### Dynamic groups in Microsoft Entra ID

You can use the enrollment **Name** field to create a dynamic group in Microsoft Entra ID. For more information, see [Microsoft Entra dynamic groups](/azure/active-directory/users-groups-roles/groups-dynamic-membership).

You can use the profile name to define the [enrollmentProfileName parameter](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) to assign devices with this enrollment profile.

Before device setup, make sure the enrolling user is a member of a Microsoft Entra user group.  

If you assign dynamic groups to enrollment profiles, there might be a delay in delivering applications and policies to devices after the enrollment.

### Setup Assistant screen reference
The following table describes the Setup Assistant screens shown during automated device enrollment for visionOS. For more information about how each Setup Assistant screen affects the user experience, see [Apple Platform Deployment guide: Manage Setup Assistant for Apple devices](https://support.apple.com/en-mide/guide/deployment/depdeff4a547/web) (opens Apple support site).  

| Setup Assistant screen | What happens when visible |
|------------------------------------------|------------------------------------------|
| **Passcode** | Shows the passcode and password lock pane to users, and prompts users for a passcode. Always require a passcode for unsecured devices unless access is controlled in some other way (such as through a kiosk mode configuration that restricts the device to one app). |
| **Location Services** | Shows the location services setup pane, where users can enable location services on their device. |
| **Restore** | Shows the apps and data setup pane. On this screen, users setting up devices can restore or transfer data from iCloud Backup. |
| **Apple ID** | Shows the Apple ID setup pane, which gives users the option to sign in with their Apple ID and use iCloud. |
| **Terms and conditions** | Shows the Apple terms and conditions pane, and requires users to accept them. |
| **Optic ID** | Shows the biometric setup pane, which gives users the option to set up Optic ID on their devices. |
| **Siri** | Shows the Siri setup pane to users. |
| **Diagnostics Data** | Shows the diagnostics pane where users can opt in to send diagnostic data to Apple. |
| **Privacy** | Shows the privacy setup pane to the user. |
| **Screen Time** | Shows the Screen Time screen. |
| **Software Update** | Shows the mandatory software update screen. |
| **Appearance** | Shows the appearance setup pane. |
| **Device to Device Migration** | Shows the device-to-device migration pane. On this screen, users can transfer data from an old device to their current device. |
| **Accessibility** | Shows the accessibility setup pane, where users can configure accessibility options for visionOS. |
| **Intelligence** | Shows the Apple Intelligence setup pane, where users can configure Apple Intelligence features. |
| **Get Started** | Shows users the Get Started pane. |

## Assign an enrollment profile to devices

Before devices can be enrolled, you need to assign an enrollment profile to them.

>[!NOTE]
>You can also assign serial numbers to profiles in the **Apple Serial Numbers** pane.

1. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices**.
1. Expand **Device onboarding**, and then select **Enrollment**.
1. Select the **Apple mobile** tab.
1. Choose **Enrollment program tokens**.
2. Select an enrollment token.
3. Select **Devices**.
5. Select all devices you want to assign, and then select **Assign profile**.
4. Under **Assign profile**, choose the automated device enrollment profile you created for the devices, and then select **Assign**.

### Assign a default profile

You can pick a default profile to be applied to all devices that enroll with a specific token.

1. In the admin center, return to **Enrollment program tokens**.
2. Select an enrollment token.
2. Select **Set Default Profile**.
4. Select a profile in the list, and then select **Save**. From here, Intune applies the profile to all devices that enroll with the selected enrollment token.

> [!NOTE]
> Ensure that **Device Type Restrictions** under **Enrollment Restrictions** doesn't have the default **All Users** policy set to block the visionOS platform. This setting causes automated enrollment to fail and your device shows as Invalid Profile, regardless of user attestation. To permit enrollment only by company-managed devices, block only personally owned devices, which permits corporate devices to enroll. Microsoft defines a corporate device as a device that's enrolled through a Device Enrollment Program or a device that's manually entered under **Corporate device identifiers**.

## Re-enroll a device
Complete these steps to re-enroll a device that already went through automated device enrollment.

1. There are two options for resetting the device:
    * Wipe the device in the Microsoft Intune admin center.
    * Retire the device in the admin center, and then reset the device to factory settings using the Settings app or Apple Configurator 2.
2. Turn on the device and follow the onscreen steps in Setup Assistant to retrieve the remote management profile.

## Next steps

- To sync devices, assign enrollment profiles, and distribute devices to users, see [Manage ADE devices](manage-devices-tokens-apple.md).
- To renew or delete your enrollment program token, see [Set up an ADE token](setup-apple-token.md).
- For troubleshooting, see [Troubleshoot iOS/iPadOS device enrollment problems](/troubleshoot/mem/intune/troubleshoot-ios-enrollment-errors#error-messages).
