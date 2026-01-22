---
title: Move from Basic Mobility and Security to Intune: Migration Guide
description: Follow this migration guide to move your mobile device management from Microsoft 365 Basic Mobility and Security to Intune. Includes policy mapping and license assignment steps.
author: MandiOhlinger
ms.author: mandia
ms.date: 01/22/2026
ms.topic: how-to
ms.reviewer: jamiesil, dagerrit
ms.collection:
- M365-identity-device-management
---

# Move to Intune from Microsoft 365 Basic Mobility and Security

**Basic Mobility and Security** is a basic set of policies included with Microsoft 365 that help protect devices that access Microsoft 365 apps, like Outlook.

Many organizations want more advanced device management features that Microsoft Intune provides. For a comparison of the features, see [Choose between Basic Mobility and Security or Intune](/microsoft-365/admin/basic-mobility-security/choose-between-basic-mobility-and-security-and-intune).

If you use Basic Mobility and Security and want to move to Intune, this article helps you through the process. Moving to Intune requires the following major steps, which are described in more detail in this article:

1. **Prepare**:

    Review your Intune licenses, Basic Mobility and Security policies, group memberships, and devices to streamline the move.

2. **Evaluate and migrate your existing policies**:

    Use the policy mapping guidance to create new Intune policies that correspond to your existing Basic Mobility and Security policies.

3. **Assign the policies and complete the move**:

    Assign the Intune licenses to users or groups, which automatically switches the users to Intune device management. When you assign licenses, users and devices are ready to receive the new Intune policies you create.

4. **Configure more settings**:

    After you move to Intune, create more policies to take advantage of the different Intune features.

This article helps you move your mobile device management (MDM) from Microsoft 365 Basic Mobility and Security to Microsoft Intune.

## Before you begin

- When you sign in to the admin centers, use an account with the following roles:

  - **License administrator** - This Microsoft Entra role lets you assign Intune licenses in the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854). For more information on this role, see [Microsoft Entra built-in roles - License Administrator](/entra/identity/role-based-access-control/permissions-reference#license-administrator).

  - **Policy and profile manager** - This Microsoft Intune role lets you create and assign policies in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). For more information on this role, see [Built-in roles for Microsoft Intune](../fundamentals/role-based-access-control-reference.md#policy-and-profile-manager).

- Test the steps in this article on a test users group that have devices enrolled in Basic Mobility and Security. Confirm that the policies behave as you expect.

- After you move to Intune, the existing Basic Mobility and Security policies are still available and shown in [Basic Mobility and Security](https://compliance.microsoft.com/basicmobilityandsecurity). However, the Basic Mobility and Security policies no longer apply to users that are assigned Intune licenses.

  Microsoft recommends that you remove the Basic Mobility and Security policies. You don't want these old policies to accidentally get assigned to users later. For more information, see [Turn off Basic Mobility and Security enforcement](/microsoft-365/admin/security-and-compliance/m365b-devices-basic-mobility-security-turn-off).

## Step 1 - Prepare

For more information, see [Basic Mobility and Security overview](/microsoft-365/admin/security-and-compliance/m365b-devices-basic-mobility-security-overview).

Before you move from Basic Mobility and Security device management to Intune device management:

1. Make sure you have enough [Intune licenses](licenses.md) to cover all your users managed by Basic Mobility and Security. If you don't have enough licenses, group your users by priority and assign licenses in stages.
1. Review the existing Basic Mobility and Security policies and delete any policies that you no longer need. Deleting unneeded policies reduces the number of new Intune policies you create.

    The following articles list and describe the Basic Mobility and Security policies:

    - [Set up Basic Mobility and Security](/microsoft-365/admin/security-and-compliance/m365b-devices-basic-mobility-security-set-up)
    - [Configure policies in Basic Mobility and Security](/microsoft-365/admin/security-and-compliance/m365b-devices-basic-mobility-security-policies-configure)

    If users are already licensed for Intune, they can get Intune policies assigned sooner than expected and their devices can lose any Basic Mobility and Security configurations.

1. Review the group memberships that are currently assigned device security policies. When you set up Basic Mobility and Security, you assigned policies to groups by using the steps at [Set up Basic Mobility and Security](/microsoft-365/admin/security-and-compliance/m365b-devices-basic-mobility-security-set-up#step-4-configure-organization-settings-in-basic-mobility-and-security).

    Decide if you plan to use the same groups for your Intune policies or create new groups. If these groups include users that are already licensed for Intune, they can get Intune policies assigned sooner than expected.

1. Review the types of devices currently enrolled in Basic Mobility and Security. Unsupported [OS versions and variants](supported-devices-browsers.md#intune-supported-operating-systems) might continue to work, but they're not supported in Intune.

1. Be ready to create new Intune policies in the Intune admin center. These policies replace the Basic Mobility and Security policies.

## Step 2 - Evaluate existing policies and create new Intune policies

After you prepare your licenses and review the information in [Step 1 - Prepare](#step-1---prepare), use the policy mapping lists to create new Intune policies. The Intune policies should correspond to your existing Basic Mobility and Security policies.

1. In [Basic Mobility and Security](https://compliance.microsoft.com/basicmobilityandsecurity), review each Basic Mobility and Security policy. Use the following policy mapping references and compare them with the Intune policies. If you haven't already, decide which policies you want to create in Intune.

    - [Access requirements policy mapping](policy-map-access-requirements.md)
    - [Configurations policy mapping](policy-map-configurations.md)
    - [Miscellaneous policy mapping](policy-map-miscellaneous.md)

2. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create your Intune policies based on the policy mappings. When you create the policies, you can assign them to your groups now, or assign them later.

    | Basic Mobility and Security policy | Intune policy type | Intune location |
    | --- | --- | --- |
    | [Access requirements policy mapping](policy-map-access-requirements.md) | [Compliance policies](../protect/device-compliance-get-started.md) |  [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Compliance** |
    | [Configurations policy mapping](policy-map-configurations.md) | [Device configuration profiles](../configuration/device-profiles.md) | [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Manage devices** > **Configuration** |
    | [Miscellaneous policy mapping](policy-map-miscellaneous.md) | [Device configuration profiles](../configuration/device-profiles.md) | [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Manage devices** > **Configuration** |
    | Basic Conditional Access policies described at [Set up Basic Mobility and Security](/microsoft-365/admin/security-and-compliance/m365b-devices-basic-mobility-security-set-up) and [Configure policies in Basic Mobility and Security](/microsoft-365/admin/security-and-compliance/m365b-devices-basic-mobility-security-policies-configure). | [Conditional Access policies]( ../protect/conditional-access.md) | [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Conditional Access** > **Classic policies** <br/><br/>Conditional Access is a Microsoft Entra feature. |

## Step 3 - Assign the policies in stages

Next, assign the Intune policies to the groups you choose. Keep the following points in mind:

- If you already assigned Intune policies to your groups, these policies can conflict with your new Intune policies. To learn how Intune handles conflicts, see [Common questions and answers with device policies and profiles in Microsoft Intune](../configuration/device-profile-troubleshoot.md#compliance-and-device-configuration-policies-that-conflict).

- When the Intune policies are created, you can assign them to groups at any time. We recommend assigning the policies in stages. This staged approach helps you manage the migration process.

- After you assign your Intune policies to these groups, all Intune licensed users in the groups receive the policies, even users not previously managed by Basic Mobility and Security.

### Assign the policies

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select your policy > **Assignments** > **Edit**. Add your groups and **Save**. When you save, the policies are assigned.

    For the steps and guidance, see [Assign policies in Microsoft Intune](../configuration/device-profile-assign.md).

    It's important to understand how policy assignment works. When you assign Intune licenses, the Intune policies replace any existing Basic Mobility and Security policies. Users can lose settings and email configuration if they're licensed for Intune but not assigned to any Intune policies.

    Remember, the Intune license assignment is a key step in the move from Basic Mobility and Security to Intune device management.

2. For users without Intune licenses, assign Intune licenses to the users and groups you want to move to Intune. You can assign Intune licenses in the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854):

    - Assign licenses to **Users**. For more information, see [Assign licenses to users](/microsoft-365/admin/manage/assign-licenses-to-users).
    - Assign licenses to **Groups**. For more information, see [Assign licenses to a group](/microsoft-365/admin/manage/manage-group-licenses).

    For more information on assigning licenses in Intune, see [Assign licenses to users so they can enroll devices in Intune](licenses-assign.md).

At the next [Intune device refresh cycle](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals), the devices automatically switch to Intune management and the new policies start affecting user devices.

After you move to Intune, Microsoft recommends that you remove the Basic Mobility and Security policies. You don't want these old policies to accidentally get assigned to users later. To learn more, see [Turn off Basic Mobility and Security enforcement](/microsoft-365/admin/security-and-compliance/m365b-devices-basic-mobility-security-turn-off).

## Step 4 - Configure more settings

The Basic Mobility and Security policies are a basic set of device management settings. After you migrate to Intune, you can create more policies to take advantage of the different Intune features.

For information on a recommended minimum base set of policies, see [Get started with Intune](get-started-with-intune.md).

To summarize, you can:

- Continue with basic set of Intune policies that protect devices and protect Microsoft 365 apps.
- Create more Intune policies to take advantage of the other features available to you.

## Related articles

- [What is Intune?](what-is-intune.md)
- [Get started with Intune](get-started-with-intune.md)
