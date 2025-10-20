---
title: Set up enrollment time grouping
description: Overview and setup of the enrollment time grouping feature in Microsoft Intune.
ms.date: 04/15/2025
ms.topic: how-to
ms.reviewer:
ms.collection:
- M365-identity-device-management
- highpri
- highseo
---

# Enrollment time grouping in Microsoft Intune

**Applies to:**
* Windows 11
* Android

Set up enrollment time grouping to speed up app and policy provisioning during device enrollment. With enrollment time grouping, you can add a Microsoft Entra security group in the enrollment profile so that devices are added to the group during enrollment, rather than after. You can then assign required apps and policy configuration to the group. This preknowledge of the security group that the device will become member of after enrollment enables Intune to deliver the configurations to the device quickly on enrollment, reducing post-enrollment latency and improving time to productivity.

If you don't configure enrollment time grouping, enrolled devices are grouped based on inventory properties and group tag IDs. Then Microsoft Intune delivers apps and policies based on the group membership. Microsoft Intune can only determine the apps and policies a device needs after the device is grouped, so devices grouped this way often aren't ready for immediate use. It can take up to 8 hours post enrollment for devices to receive all apps and policies.

This article provides an overview of enrollment time grouping, how to configure it, and feature limitations.

## Prerequisites

Enrollment time grouping is supported on devices provisioned via:

* [Windows Autopilot device preparation](/autopilot/device-preparation/overview)

* [Android Enterprise](../fundamentals/deployment-guide-enrollment-android.md)

For Windows Autopilot, you must have permissions to create and modify Windows Autopilot device preparation policies. To configure Microsoft Entra groups in an enrollment profile, you must have the *enrollment time device membership assignment* permission. This permission is available for custom roles, under the **Enrollment programs** category in the Microsoft Intune admin center.

For Android Enterprise, you must have permissions to create and modify Android Enterprise enrollment profiles. To configure Microsoft Entra groups in an Android enrollment profile, you must have the *enrollment time device membership assignment for Android Enterprise* permission. This permission is available for custom roles, under the __Android Enterprise__ category in the Microsoft Intune admin center. Enrollment time grouping is supported with the following enrollment profiles:

* Android Enterprise fully managed

* Android Enterprise corporate-owned work profile

* Android Enterprise dedicated

>[!TIP]
> For more information about creating custom roles, see [Role based access control](../fundamentals/role-based-access-control.md#custom-roles).

To add Intune first party app as a security group owner, which is a required step for enrollment time grouping, you must meet one of the following prerequisites:
  * Must be a Microsoft Entra Group Administrator, or another role with the *microsoft.directory/groups/owners/update* permission.
  * Must be an existing owner of the Microsoft Entra security group.

Lastly, the designated group should be configured as a scope group for the admin to use it in enrollment time grouping configuration.

## Step 1: Create Microsoft Entra security group

Create a static Microsoft Entra security group for use in enrollment profiles. To configure enrollment time grouping, you must add the Intune Provisioning Client as an owner of the security group. You don't need to add devices or users to this group right now.

The following procedure describes how to create a security group in the Microsoft Intune admin center. For more information and steps specific to Windows 11, see [Windows Autopilot - Create a device group](/autopilot/device-preparation/tutorial/user-driven/entra-join-device-group#create-a-device-group).

After you configure enrollment time grouping in the enrollment profile, you can come back to this security group to add and remove devices. Any Intune administrator with the appropriate security group permissions can edit the security group.

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. Go to **Groups**.

1. Select **All groups**, and then select **New group**.

1. On the **New Group** screen that opens, enter the following information:

    1. **Group type**: Select **Security**.

    1. **Group name**: Enter a name for the device group. Example: *Shared inventory devices*

    1. **Group description**: Enter a description for the device group.

    1. **Microsoft Entra roles can be assigned to the group**: Select **No**.

    1. **Membership type**: Select **Assigned**.

    1. **Owners**: Select the **No owners selected** link.

    1. On the **Add owners** screen that opens, add the Intune Provisioning Client as owner:

       1. Scroll through the list of objects and select the service principal **Intune Provisioning Client** with AppId of **f1346770-5b25-470b-88bd-d5744ab7952c**. Alternatively, use the **Search** bar to search for and select **Intune Provisioning Client**.

           > [!NOTE]
           >
           > - In some tenants, the service principal might have the name of **Intune Autopilot ConfidentialClient** instead of **Intune Provisioning Client**. As long as the AppID of the service principal is **f1346770-5b25-470b-88bd-d5744ab7952c**, it's the correct service principal.
           >
           > - If the **Intune Provisioning Client** or **Intune Autopilot ConfidentialClient** service principal with AppId of **f1346770-5b25-470b-88bd-d5744ab7952c** isn't available either in the list of objects or when searching, see [Adding the Intune Provisioning Client service principal](/autopilot/device-preparation/tutorial/user-driven/entra-join-device-group#adding-the-intune-provisioning-client-service-principal) for next steps.

       1. Choose **Select**.

    1. Select **Create** to finish creating the assigned device group.

## Step 2: Configure enrollment time grouping in enrollment profile

The enrollment time grouping feature only applies to new device enrollments. It doesn't affect or apply to devices that are already enrolled.

You can add one static Microsoft Entra security group per enrollment profile. As an Intune admin, you can only add Microsoft Entra groups that are authorized in the scope group for your Intune role. Make sure [scope groups](../fundamentals/role-based-access-control.md#about-intune-role-assignments) and group tags are assigned to the appropriate roles so that admins can see the security group during profile creation.

1. In the Microsoft Intune admin center, go to **Devices**.
1. Expand **Device onboarding**, and then select **Enrollment**.
1. Select the type of enrollment you're configuring and create a profile.

   - Windows: [Create Windows Autopilot device preparation policy](/autopilot/device-preparation/tutorial/user-driven/entra-join-autopilot-policy)

   - Android Enterprise with work profile: [Set up Intune enrollment of Android Enterprise corporate-owned devices with work profile](/intune/intune-service/enrollment/android-corporate-owned-work-profile-enroll)

   - Android Enterprise dedicated: [Set up Intune enrollment of Android Enterprise dedicated devices](/intune/intune-service/enrollment/android-kiosk-enroll)

   - Android Enterprise fully managed: [Set up enrollment for Android Enterprise fully managed devices](/intune/intune-service/enrollment/android-fully-managed-enroll)

    >[!TIP]
    > Enrollment time grouping isn't supported with the staging token. If you're configuring a profile for use with enrollment time grouping, use the corporate-owned, fully managed (default) token or the corporate owned work profile (default) token.

After you save the profile, you can return to it at any time to edit group settings. Updates you make to the group settings don't apply to devices already enrolled with the profile. If you remove a device from the group, Microsoft Intune reevaluates policy configurations and forces the device to check in to obtain new configurations.

## Step 3: Enroll devices

When devices assigned the enrollment profile enroll, they become members of the Microsoft Entra security group and start receiving apps and policies. After the admin or end user completes the initial device setup, they land on the home screen of the device. At this point, all targeted apps and policies should already be on the device or in the process of being installed.

If you remove a device from the group, Microsoft Intune reevaluates policy configurations and forces the device to check in to obtain new configurations.

## Known issues and limitations

Reporting for enrollment time grouping isn't currently available.

## Troubleshooting

If unexpected behavior occurs, contact Microsoft Support with the following information:

- Device serial number.
- Company Portal app logs, if applicable, with log ID.
- Approximate time stamp of the event and time zone where it happened.
- Screenshots from the Microsoft Intune admin center or device.
- Detailed explanation of the behavior on the device.
