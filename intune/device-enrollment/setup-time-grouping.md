---
title: Set up enrollment time grouping
description: Overview and setup of the enrollment time grouping feature in Microsoft Intune.
ms.date: 05/18/2026
ms.topic: how-to
ms.reviewer:
ms.collection:
- M365-identity-device-management
---

# Enrollment time grouping in Microsoft Intune

Set up enrollment time grouping to speed up app and policy provisioning during device enrollment. With enrollment time grouping, you can add a Microsoft Entra security group in the enrollment policy so that devices are added to the group during enrollment, rather than after. You can then assign required apps and policy configuration to the group. This preknowledge of the security group that the device will become member of after enrollment enables Intune to deliver the configurations to the device quickly on enrollment, reducing post-enrollment latency and improving time to productivity.

If you don't configure enrollment time grouping, enrolled devices are grouped based on inventory properties and group tag IDs. Then Microsoft Intune delivers apps and policies based on the group membership. Microsoft Intune can only determine the apps and policies a device needs after the device is grouped, so devices grouped this way often aren't ready for immediate use. It can take up to 8 hours post enrollment for devices to receive all apps and policies.

This article provides an overview of enrollment time grouping, how to configure it, and feature limitations.

## Requirements

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> Enrollment time grouping is supported on the following platforms:
>
> - Android Enterprise
> - iOS/iPadOS
> - macOS
> - tvOS
> - visionOS
> - Windows 11

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [enrollment-methods](../includes/requirements/enrollment-methods.md)]

:::column-end:::
:::column span="3":::

> Enrollment time grouping is supported on devices provisioned via:
>
> - [Automated device enrollment for iOS/iPadOS, tvOS, and visionOS](./apple/overview-automated-enrollment-apple.md)
> - [Automated device enrollment for macOS](./apple/overview-automated-enrollment-macos.md)
> - [Windows Autopilot device preparation](/autopilot/device-preparation/overview)
> - [Android Enterprise](android/guide.md)
>
> For iOS/iPadOS automated device enrollment, enrollment time grouping is supported with the following authentication methods:
>
> - Enrollment with user affinity:
>   - Setup Assistant with modern authentication
>   - Company Portal
> - Enrollment without user affinity:
>   - Enroll with Microsoft Entra shared mode
>   - Enroll with shared iPad
>
> For macOS automated device enrollment, enrollment time grouping is supported with the following authentication methods:
>
> - Enrollment with user affinity:
>   - Setup Assistant with modern authentication
> - Enrollment without user affinity
>
> For Android Enterprise, enrollment time grouping is supported with the following enrollment policies:
>
> - Android Enterprise fully managed
> - Android Enterprise corporate-owned work profile
> - Android Enterprise dedicated

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::

> The permissions you need depend on the platform you're configuring:
>
> - iOS/iPadOS, tvOS, and visionOS automated device enrollment: Permissions to create and modify iOS/iPadOS, tvOS, and visionOS enrollment policies, and the *enrollment time device membership assignment* permission (available in custom roles under **Enrollment programs**).
> - macOS automated device enrollment: Permissions to create and modify macOS enrollment policies, and the *enrollment time device membership assignment* permission (available in custom roles under **Enrollment programs**).
> - Windows Autopilot: Permissions to create and modify Windows Autopilot device preparation policies, and the *enrollment time device membership assignment* permission (available in custom roles under **Enrollment programs**).
> - Android Enterprise: Permissions to create and modify Android Enterprise enrollment policies, and the *enrollment time device membership assignment for Android Enterprise* permission (available in custom roles under **Android Enterprise**).
>
> To add the Intune first-party app as a security group owner, you must be a Microsoft Entra Group Administrator (or hold the *microsoft.directory/groups/owners/update* permission), or be an existing owner of the security group.
>
> The designated group must be configured as a scope group for the admin to use it in enrollment time grouping configuration.


:::column-end:::
:::row-end:::  

> [!TIP]
> For more information about creating custom roles, see [Role based access control](../fundamentals/role-based-access-control/overview.md#custom-roles).

## Step 1: Create Microsoft Entra security group

Create a static Microsoft Entra security group for use in enrollment policies. To configure enrollment time grouping, you must add the Intune Provisioning Client as an owner of the security group. You don't need to add devices or users to this group right now.

The following procedure describes how to create a security group in the Microsoft Intune admin center. For more information and steps specific to Windows 11, see [Windows Autopilot - Create a device group](/autopilot/device-preparation/tutorial/user-driven/entra-join-device-group#create-a-device-group).

After you configure enrollment time grouping in the enrollment policy, you can come back to this security group to add and remove devices. Any Intune administrator with the appropriate security group permissions can edit the security group.

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

## Step 2: Configure enrollment time grouping in enrollment policy

The enrollment time grouping feature only applies to new device enrollments. It doesn't affect or apply to devices that are already enrolled.

You can add one static Microsoft Entra security group per enrollment policy. As an Intune admin, you can only add Microsoft Entra groups that are authorized in the scope group for your Intune role. Make sure [scope groups](../fundamentals/role-based-access-control/overview.md#about-intune-role-assignments) and group tags are assigned to the appropriate roles so that admins can see the security group during policy creation.

1. In the Microsoft Intune admin center, go to **Devices**.
1. Expand **Device onboarding**, and then select **Enrollment**.
1. Select the type of enrollment you're configuring and create a policy.

   - iOS/iPadOS: [Set up automated device enrollment for iOS/iPadOS](apple/setup-automated-ios.md)

   - macOS: [Set up automated device enrollment for macOS](apple/setup-automated-macos.md)

   - Windows: [Create Windows Autopilot device preparation policy](/autopilot/device-preparation/tutorial/user-driven/entra-join-autopilot-policy)

   - Android Enterprise with work profile: [Set up Intune enrollment of Android Enterprise corporate-owned devices with work profile](android/setup-corporate-work-profile.md)

   - Android Enterprise dedicated: [Set up Intune enrollment of Android Enterprise dedicated devices](android/setup-dedicated.md)

   - Android Enterprise fully managed: [Set up enrollment for Android Enterprise fully managed devices](android/setup-fully-managed.md)

   - tvOS: [Set up enrollment policy for tvOS](apple/setup-automated-tv-os.md)  

   - visionOS: [Set up enrollment policy visionOS](apple/setup-automated-vision-os.md) 

    >[!TIP]
    > Enrollment time grouping isn't supported with the staging token. If you're configuring a policy for use with enrollment time grouping, use the corporate-owned, fully managed (default) token or the corporate owned work profile (default) token.

After you save the policy, you can return to it at any time to edit group settings. Updates you make to the group settings don't apply to devices already enrolled with the policy. If you remove a device from the group, Microsoft Intune reevaluates policy configurations and forces the device to check in to obtain new configurations.

## Step 3: Enroll devices

When devices assigned the enrollment policy enroll, they become members of the Microsoft Entra security group and start receiving apps and policies. After the admin or end user completes the initial device setup, they land on the home screen of the device. At this point, all targeted apps and policies should already be on the device or in the process of being installed.

If you remove a device from the group, Microsoft Intune reevaluates policy configurations and forces the device to check in to obtain new configurations.  

## Reporting  

To access reporting for enrollment time grouping, go to **Devices** > **Monitor** > **Enrollment time grouping failures**. The available report shows only failures. Specifically, information about devices that failed to become members of a specific static device group during these setup processes:  

- Windows Autopilot preparation provisioning  
- Android Enterprise fully managed enrollment  
- Android Enterprise corporate-owned work profile enrollment  
- Android Enterprise dedicated enrollment  
- Apple mobile automated device enrollment  

Recently updated information can take up to 20 minutes to appear in the report. You must have the *Microsoft.Intune/ManagedDevices/Read* RBAC permission to view the report.

> [!IMPORTANT]
> This report provides awareness about devices that fail to be added to the security groups configured in the enrollment policies. Failure to join the group during enrollment might cause configuration to change or be removed from the device after enrollment, so we recommend monitoring the report continuously so that you can take the necessary mitigating actions right away. You could, for example, use a custom app that scans the report data on a regular schedule. The app then generates a notification when it finds new devices in the report.  

## Known issues and limitations

There are no known issues or limitations with enrollment time grouping. 

## Troubleshooting

If unexpected behavior occurs, contact Microsoft Support with the following information:

- Device serial number.
- Company Portal app logs, if applicable, with log ID.
- Approximate time stamp of the event and time zone where it happened.
- Screenshots from the Microsoft Intune admin center or device.
- Detailed explanation of the behavior on the device.
