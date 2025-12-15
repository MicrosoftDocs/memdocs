---
title: Move from Microsoft 365 Basic Mobility and Security to Intune
description: Learn how to move your mobile device management from Microsoft 365 Basic Mobility and Security to Intune.
author: MandiOhlinger
ms.author: mandia
ms.date: 12/15/2025
ms.topic: how-to
ms.reviewer: jamiesil, dagerrit
ms.collection:
- M365-identity-device-management
---

# Move to Intune from Microsoft 365 Basic Mobility and Security

Microsoft 365 includes a basic set of policies that help protect devices and Microsoft 365 apps, like Outlook. These policies are managed in the Microsoft Defender portal and are called **Basic Mobility and Security**.

Many organizations want more or next-level device management features. Specifically, they want the features that are included with Microsoft Intune. For a comparison of the features, go to [Choose between Basic Mobility and Security or Intune](/microsoft-365/admin/basic-mobility-security/choose-between-basic-mobility-and-security-and-intune).

You can move from Basic Mobility and Security to Microsoft Intune. Moving to Intune requires the following major steps:

1. **Prepare**:

    Review your Intune licenses, Basic Mobility and Security policies, group memberships, and devices to streamline the move.

2. **Evaluate and migrate your existing policies**:

    Use the policy mapping guidance to create new Intune policies that correspond to your existing Basic Mobility and Security policies.

3. **Assign the policies and complete the move**:

    Assign licenses to users or groups, which automatically switches the users to Intune device management at the next refresh cycle. ??Is this still true? Or, will there be conflicts??

4. **Configure more settings**:

    After you move to Intune, create more policies to take advantage of the different Intune features.

This article helps you move your mobile device management (MDM) from Microsoft 365 Basic Mobility and Security to Microsoft Intune.

## Before you begin

- Previously, there was a **Migration evaluation** tool in the Microsoft Intune admin center. This tool is removed and no longer available.

- When you sign into the admin centers, you need an account with the following roles:

  - **License administrator** - This Microsoft Entra role lets you assign Intune licenses in the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854). For more information on this role, go to [Microsoft Entra built-in roles - License Administrator](/entra/identity/role-based-access-control/permissions-reference#license-administrator).

  - **Policy and profile manager** - This Microsoft Intune role lets you create and assign policies in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). For more information on this role, go to [Built-in roles for Microsoft Intune](../fundamentals/role-based-access-control-reference.md#policy-and-profile-manager).

- Test the steps in this article on a test users group that have devices enrolled in Basic Mobility and Security. Confirm that the policies behave as you expect.

??Possibly delete all bullets below??

- After you migrate to Intune, the existing device security policies deployed with Basic Mobility and Security are permanently frozen. ??Is this true??

- Assigning Intune licenses impacts the migration process. The license assignment controls the migration of devices from Basic Mobility and Security to Intune.

  Users with Intune licenses already assigned can start receiving policies immediately, possibly sooner than you expect. The policies can happen even if Basic Mobility and Security didn't previously manage the users or devices.

  If you want to prevent this behavior, you can unassign the Intune licenses before the migration. You can also create separate groups to help manage when the policies are deployed:

  - Group 1: Users with Intune licenses already assigned
  - Group 2: Users without Intune licenses assigned

  Then, you can assign the migrated Basic Mobility and Security device security policies to users who aren't assigned Intune licenses.

## Step 1 - Prepare

Before you move from Basic Mobility and Security device management to Intune device management:

1. Be sure you have enough [Intune licenses](licenses.md) to cover all your users managed by Basic Mobility and Security.
2. Review the Basic Mobility and Security [device security policies](/microsoft-365/admin/basic-mobility-security/set-up#step-4-recommended-manage-device-security-policies) in the Microsoft Defender portal. Delete any policies that are no longer needed. Deleting unneeded policies reduces the number of new Intune policies you create.
3. Review the [group memberships](/microsoft-365/admin/security-and-compliance/m365b-devices-basic-mobility-security-policies-configure#create-policies-in-basic-mobility-and-security) that are currently assigned device security policies.

    Decide if you plan to use the same groups for your Intune policies or create new groups. If these groups include users that are already licensed for Intune, then they can get policies assigned sooner than expected.

4. Review the types of devices currently enrolled in Basic Mobility and Security. Unsupported [OS versions and variants](supported-devices-browsers.md#intune-supported-operating-systems) might continue to work, but they aren't supported in Intune.

    If users are already licensed for Intune, then their devices lose any configuration set by device security policies in the Microsoft Defender portal. ??Still true??

5. Be prepared to create new Intune policies in the Intune admin center. These policies will replace the Basic Mobility and Security policies.

??After the migration evaluation process activates, you can't make changes to your device security policies in the Microsoft Defender portal. The existing Basic Mobility and Security policies are still enforced, but changes to these existing policies aren't saved. ??Still true??

## Step 2 - Evaluate existing policies and create new Intune policies

After you prepare your licenses and review the information in [Step 1 - Prepare](#step-1---prepare), the next step is to use the policy mapping lists and create new Intune policies. The Intune policies should correspond to your existing Basic Mobility and Security policies.

1. In the [Microsoft Defender portal](https://security.microsoft.com), review each Basic Mobility and Security policy. Use the following policy mapping references and compare it with the Intune policies. If you haven't already, decide which policies you want to create in Intune.

    - [Access requirements policy mapping](policy-map-access-requirements.md)
    - [Configurations policy mapping](policy-map-configurations.md)
    - [Miscellaneous policy mapping](policy-map-miscellaneous.md)

2. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create your Intune policies based on the policy mappings. When you create the policies, you can assign them to your groups now, or assign them later.

    | Basic Mobility and Security policy | Intune policy type | Intune location |
    | --- | --- | --- |
    | [Access requirements policy mapping](policy-map-access-requirements.md) | [Compliance policies](../protect/device-compliance-get-started.md) |  [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Compliance** |
    | [Configurations policy mapping](policy-map-configurations.md) | [Device configuration profiles](../configuration/device-profiles.md) | [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Manage devices** > **Configuration** |
    | [Miscellaneous policy mapping](policy-map-miscellaneous.md) | [Device configuration profiles](../configuration/device-profiles.md) | [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Manage devices** > **Configuration** |
    | ??Does BMS create CA policies? If not, I'll move this to step 4.?? | [Conditional Access policies]( ../protect/conditional-access.md)</br></br> Microsoft Entra Conditional Access blocks access if the settings aren't compliant. | [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Conditional Access** > **Classic policies** |

## Step 3 - Assign the policies in stages

The next step is to assign the policy to the groups you choose. Keep the following points in mind:

- If your groups already have Intune policies assigned to them, then these policies can conflict with your new Intune policies. To learn how conflicts are handled in Intune, go to [Common questions and answers with device policies and profiles in Microsoft Intune](../configuration/device-profile-troubleshoot.md#compliance-and-device-configuration-policies-that-conflict).

- When the policies are created, they can be assigned to groups at any time. We recommend assigning the policies in stages. This staged approach helps you manage the migration process.

- After you assign your Intune policies to these groups, all Intune licensed users in the groups receive the policies, even users not previously managed by Basic Mobility and Security.

### Assign the policies

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), assign your Intune policies to the groups. Select your policy > **Assignments** > **Edit**. Add your groups and **Save**. When you save, the policies are assigned.

    For the steps and guidance, see [Assign policies in Microsoft Intune](../configuration/device-profile-assign.md).

    ?? When you assign groups, your newly migrated Intune policies replace the device settings configured in Basic Mobility and Security. If you don't assign the groups, then devices managed by Basic Mobility and Security could lose settings and email configuration when their users are licensed for Intune. Remember, the Intune license assignment is a key step in the migration of devices from Basic Mobility and Security to Intune device management.??Still true??

2. ??Why? Is this role needed to enable coexistence??: **Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)** with Microsoft Entra **[License administrator](/entra/identity/role-based-access-control/permissions-reference#license-administrator)** rights.

3. ??Still needed??: **Enable [coexistence](mdm-authority-set.md#coexistence)**. When enabled: 

    - Users with existing Intune licenses are immediately moved to Intune and the newly migrated policies are applied at the next [Intune refresh cycle](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals).
    - For users without Intune licenses, coexistence is the second step in the migration process. They'll be moved to Intune in the next step.

4. For users without Intune licenses, assign Intune licenses to the users and groups you want to move to Intune. You can assign Intune licenses in the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854):

    - Assign licenses to **Users**. For more information, go to [Assign licenses to users](/microsoft-365/admin/manage/assign-licenses-to-users).
    - Assign licenses to **Groups**. For more information, go to [Assign licenses to a group](/microsoft-365/admin/manage/manage-group-licenses).

    For more information on assigning licenses in Intune, go to [Assign licenses to users so they can enroll devices in Intune](licenses-assign.md).

At the next [Intune device refresh cycle](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals), the devices automatically switch to Intune management and the new policies start affecting user devices.

??What happens to BMS policies when Intune policies are assigned? Should they BMS policies be unassigned and then assign Intune policies? What's the guidance that causes least disruption to end users??

## Step 4 - Configure more settings

The Basic Mobility and Security policies are a basic set of device management settings. After you migrate to Intune, you can create more policies to take advantage of the different Intune features.

For information on a recommended minimum base set of policies, go to [Get started with Intune](get-started-with-intune.md).

To summarize, you can:

- Continue with basic set of policies that protect devices and protect Microsoft 365 apps.
- Create more policies to take advantage of the Intune features available to you.

## Related articles

- [What is Intune?](what-is-intune.md)
- [Get started with Intune](get-started-with-intune.md)
