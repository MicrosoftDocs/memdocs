---
title: Set up automated device enrollment (ADE) for visionOS
description: Learn how to enroll corporate-owned Apple Vision Pro devices into Microsoft Intune with Apple Automated Device Enrollment (ADE).
ms.date: 04/29/2026
ms.topic: how-to
ms.reviewer: annovich
ai-usage: ai-assisted
ms.collection:
- M365-identity-device-management
---

# Set up automated device enrollment for visionOS

*Applies to visionOS*

This article describes how to create a visionOS enrollment policy for Apple automated device enrollment (ADE) in Microsoft Intune. This type of enrollment policy is for devices without user affinity. Device setup is completed through Apple Setup Assistant and device-targeted policies are applied after enrollment. 

For an overview of ADE and its features, see [Overview of Apple Automated Device Enrollment](overview-automated-enrollment-apple.md).  


## Limitations  
  
- Enrollment occurs without user affinity.   
- Compliance policies aren't supported.  
- Setup Assistant screens can't be configured in enrollment policies.  
- Only custom configuration profiles uploaded through the settings catalog are supported for tvOS.   
- In the admin center, hardware inventory for visionOS devices enrolled through ADE currently shows the storage capacity value as 0. This value doesn't reflect the actual available device storage.   

## Prerequisites
Before you create the enrollment policy, you must have:

* Access to [Apple Business portal](https://business.apple.com/) or [Apple School Manager portal](https://school.apple.com/).
* An active Apple token (.p7m file). For steps, see [Set up an ADE token](setup-apple-token.md).
* An [Apple MDM push certificate in Intune](create-mdm-push-certificate.md).
* New or wiped Apple Vision Pro devices added to Apple Business or Apple School Manager.
     > [!Tip]
     > Automated device enrollment applies device configurations that a device user may not be able to remove. Wipe all devices prior to enrollment to return them to an out-of-box state.


## Create an enrollment policy

Create a visionOS enrollment policy for userless automated device enrollment. A device enrollment policy defines the settings applied to a group of devices during enrollment. 

> [!NOTE]
> Devices are blocked from enrolling when there aren't enough Company Portal licenses for a VPP token or if the token expires. Intune alerts you when a token is about to expire or licenses are running low.

1. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices**.
1. Expand **Device onboarding**, and then select **Enrollment**.
1. Select the **Apple mobile** tab.
1. Choose **Enrollment program tokens**.
1. Choose a token, and then select **Enrollment policies**.
1. Select **Create policies** > **visionOS**.
1. For **Basics**, give the profile a **Name** and **Description** for administrative purposes. Users don't see these details.
1. Select **Next**.

   > [!IMPORTANT]
   > You must assign an enrollment policy to your devices before the devices become active. We recommend that you set a default enrollment policy as soon as possible so that as devices sync from Apple Business or Apple School Manager, and then turn on, they can enroll correctly through automated device enrollment. If a device you synced from Apple isn't assigned an enrollment policy and someone turns it on to set it up, enrollment fails.

    > [!IMPORTANT]
    > If you make changes to an existing enrollment policy, the new settings won't take effect on assigned devices until devices are reset back to factory settings and reactivated. 

1. In the **Locked enrollment** list, select **Yes** or **No**. Locked enrollment disables visionOS settings that allow the management profile to be removed. If you enable locked enrollment, users won't be able to unenroll their device.  

1. If you selected **Allow Apple Configurator by certificate** in the previous step, choose an Apple Configurator certificate (.cer extension) to import. The limit is 10 certificates.

1. For **Await final configuration**, your options are:
      * **Yes**: Enable a locked experience at the end of Setup Assistant to ensure your most critical device configuration policies are installed on the device. Just before the home screen loads, Setup Assistant pauses and lets Intune check in with the device. The end-user experience locks while users await final configurations.

         The amount of time that users are held on the Awaiting final configuration screen varies, and depends on the total number of policies and apps you apply to the device. The more policies and apps assigned to the device, the longer the waiting time. Setup Assistant and Microsoft Intune don't enforce a minimum or maximum time limit during this portion of setup.

           >[!NOTE]
           > Only device configuration policies start installing during the awaiting final configuration screen. Apps might not install during await final configuration.  

         This setting is applied once during the out-of-box automated device enrollment experience in Setup Assistant. The device user doesn't experience it again unless they re-enroll their device. **Yes** is the default setting for new enrollment policies.

      * **No**: The device is released to the home screen when Setup Assistant ends, regardless of policy installation status. Device users might be able to access the home screen or change device settings before all policies are installed. **No** is the default setting for existing enrollment policies. 

1. Select **Next**.

1. On the **Setup Assistant** tab, configure the following profile settings:

    | Department setting | Description |
    |---|---|
    | **Department** | Appears when users tap **About Configuration** during activation. |
    |    **Department Phone**     | Appears when users tap the **Need Help** button during activation. |


1. Select **Next**.

1. To save the profile, select **Create**.

<a name='dynamic-groups-in-azure-active-directory'></a>

### Dynamic groups in Microsoft Entra ID

You can use the enrollment **Name** field to create a dynamic group in Microsoft Entra ID. For more information, see [Microsoft Entra dynamic groups](/azure/active-directory/users-groups-roles/groups-dynamic-membership).

You can use the profile name to define the [enrollmentProfileName parameter](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) to assign devices with this enrollment policy.

Before device setup, make sure the enrolling user is a member of a Microsoft Entra user group.  

If you assign dynamic groups to enrollment policies, there might be a delay in delivering applications and policies to devices after the enrollment.  

## Assign an enrollment policy to devices

Before devices can be enrolled, you need to assign an enrollment policy to them.

>[!NOTE]
>You can also assign serial numbers to profiles in the **Apple Serial Numbers** pane.

1. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices**.
1. Expand **Device onboarding**, and then select **Enrollment**.
1. Select the **Apple mobile** tab.
1. Choose **Enrollment program tokens**.
2. Select an enrollment token.
3. Select **Devices**.
5. Select all devices you want to assign, and then select **Assign policy**.
4. Under **Assign policy**, choose the automated device enrollment policy you created for the devices, and then select **Assign**.

### Assign a default policy

You can pick a default policy to be applied to all devices that enroll with a specific token.

1. In the admin center, return to **Enrollment program tokens**.
2. Select an enrollment token.
2. Select **Set Default Policy**.
4. Select a profile in the list, and then select **Save**. From here, Intune applies the profile to all devices that enroll with the selected enrollment token.  

You can also set a policy as default from your list of enrollment policies. 
1. Go to **Enrollment program tokens**.
1. Select an enrollment token. 
1. Select **Enrollment policies**.  
1. Select the menu (**...***) next to any policy. 
1. Set it as the default policy.  

> [!NOTE]
> Ensure that **Device Type Restrictions** under **Enrollment Restrictions** doesn't have the default **All Users** policy set to block the visionOS platform. This setting causes automated enrollment to fail and your device shows as Invalid Profile, regardless of user attestation. To permit enrollment only by company-managed devices, block only personally owned devices, which permits corporate devices to enroll. Microsoft defines a corporate device as a device that's enrolled through a Device Enrollment Program or a device that's manually entered under **Corporate device identifiers**.  

## Next steps

- To sync devices, assign enrollment policies, and distribute devices to users, see [Manage ADE devices](manage-devices-tokens-apple.md).

- To renew or delete your enrollment program token, see [Set up an ADE token](setup-apple-token.md). 

- Devices can receive custom configuration profiles uploaded as .plist files. For more information, see [Create a custom configuration policy](../../device-configuration/templates/configure-custom-settings.md).  
 
- Available remote device actions are the same as those available to iOS/iPadOS ADE devices. For more information, see [Remote device actions](../../device-management/actions/index.md).  
