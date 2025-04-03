---
# required metadata

title: Migrate from Microsoft 365 Basic Mobility and Security to Intune
titleSuffix: Microsoft Intune
description: Learn how to migrate your mobile device management from Microsoft 365 Basic Mobility and Security to Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/25/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier2
- M365-identity-device-management
---

# Migrate from Microsoft 365 Basic Mobility and Security to Intune

Microsoft 365 includes a basic set of policies that protect devices and protect Microsoft 365 apps, like Outlook. These policies are managed in the Microsoft Defender portal and are called **Basic Mobility and Security**. For more information on what Basic Mobility and Security offers, go to [Capabilities of Basic Mobility and Security](/microsoft-365/admin/basic-mobility-security/capabilities).

Many organizations want more or next-level device management features. Specifically, they want the features that are included with Microsoft Intune. For a comparison of the features, go to [Choose between Basic Mobility and Security or Intune](/microsoft-365/admin/basic-mobility-security/choose-between-basic-mobility-and-security-and-intune).

You can migrate from Basic Mobility and Security to Microsoft Intune. Migrating to Intune requires the following major steps:

1. **Prepare**:

    Review your Intune licenses, Basic Mobility and Security policies, group memberships, and devices to streamline the migration.

2. **Evaluate and migrate your existing policies**:

    Use the **Migration evaluation** in the [Microsoft Intune admin center](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/MifoPolicyListBlade). The output shows Intune policy and group recommendations that replace the Basic Mobility and Security policies.

3. **Assign the policies and complete the migration**:

    Assign licenses to users or groups, which will automatically switch the users to Intune device management at the next refresh cycle.

This article helps you migrate your mobile device management (MDM) from Microsoft 365 Basic Mobility and Security to Microsoft Intune.

## Before you begin

- When you sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), use an account that has Microsoft Entra **License administrator** rights. For more information on this role, go to [Microsoft Entra built-in roles - License Administrator](/entra/identity/role-based-access-control/permissions-reference#license-administrator).

- Test the steps in this article on a test users group that have devices enrolled in Basic Mobility and Security. Confirm that the policies behave as you expect.

- After you migrate to Intune, the existing device security policies deployed with Basic Mobility and Security are permanently frozen.

- Assigning Intune licenses impacts the migration process. The license assignment controls the migration of devices from Basic Mobility and Security to Intune.

  Users with Intune licenses already assigned can start receiving policies immediately, possibly sooner than you expect. The policies can happen even if Basic Mobility and Security didn't previously manage the users or devices.

  If you want to prevent this behavior, you can unassign the Intune licenses before the migration. You can also create separate groups to help manage when the policies are deployed:
  
  - Group 1: Users with Intune licenses already assigned
  - Group 2: Users without Intune licenses assigned

  Then, you can assign the migrated Basic Mobility and Security device security policies to users who aren't assigned Intune licenses.

## Step 1 - Prepare

Before you migrate from Basic Mobility and Security device management to Intune device management:

1. Be sure you have enough [Intune licenses](licenses.md) to cover all your users managed by Basic Mobility and Security.
2. Review the [device security policies](/microsoft-365/admin/basic-mobility-security/set-up#step-4-recommended-manage-device-security-policies) in the Microsoft Defender portal. Delete any policies that are no longer needed. Deleting unneeded policies reduces the number of recommendations created by the Intune migration evaluation. The idea is to have fewer recommendations to review after the migration evaluation.
3. Review the [membership of groups](/microsoft-365/admin/basic-mobility-security/create-device-security-policies#step-3-deploy-a-policy-to-your-organization) that are currently assigned device security policies.

    If these groups include users that are already licensed for Intune, then they can get policies assigned sooner than expected. For more information on the impact of existing Intune licenses, go to [Before you begin](#before-you-begin) (in this article).

4. Review the types of devices currently enrolled in Basic Mobility and Security. Unsupported [OS versions and variants](supported-devices-browsers.md#intune-supported-operating-systems) may continue to work, but they aren't supported if migrated to Intune.

    Settings applied to unsupported operating systems aren't moved to Intune. And if the user is already licensed for Intune, then their devices lose any configuration set by device security policies in the Microsoft Defender portal.

5. Before migration:

    - Don't assign Intune licenses to users whose devices are managed by Basic Mobility and Security.
    - Don't assign Intune licenses to enable [app protection policies](../apps/app-protection-policy.md), also known as mobile application management (MAM).

    Only assign Intune licenses to users after the policy migration is complete. For more information on the impact of Intune licenses, go to [Before you begin](#before-you-begin) (in this article).

6. You may have to create new Intune policies to replace Basic Mobility and Security policies. For more information on a minimum base set of policies, go to [Get started with Intune](get-started-with-intune.md).

After the migration evaluation process activates, you can't make changes to your device security policies in the Microsoft Defender portal. The existing Basic Mobility and Security policies are still enforced, but changes to these existing policies aren't saved.

> [!IMPORTANT]
> If you have any of the following products or service, then contact the support team before you proceed:
>
> - Enterprise Mobility + Security A3 for Faculty
> - Enterprise Mobility + Security A3 for Students
> - Enterprise Mobility + Security A3 for students use benefit
> - Enterprise Mobility + Security A5 for Faculty
> - Enterprise Mobility + Security A5 for Students
> - Enterprise Mobility + Security A5 for students use benefit
> - Intune for Education
> - Intune for Education Add-On
> - Microsoft Intune for Education for Faculty
> - Microsoft Intune for Education for Student
> - Microsoft Intune for Education Prepaid Device

## Step 2 - Evaluate and migrate your existing policies

After you've prepared your licenses and reviewed the information in [Step 1 - Prepare](#step-1---prepare), use the [Microsoft Intune admin center Migration evaluation](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/MifoPolicyListBlade) to get Intune policy recommendations.

The tool can migrate your existing Basic Mobility and Security device security policies to Intune as [compliance policies](../protect/device-compliance-get-started.md) and [device configuration profiles](../configuration/device-profiles.md). It also makes recommendations for which groups the new policies should be assigned.

These Intune recommendations are designed to replicate the Basic Mobility and Security policies. **You need to review these recommendations** to make sure they reflect the old policies.

To evaluate and migrate policies from Basic Mobility and Security to Intune:

1. Complete the steps in the [Step 1 - Prepare](#step-1---prepare) section (in this article).
2. Open the [Migration evaluation](https://intune.microsoft.com/#blade/Microsoft_Intune_Workflows/MifoPolicyListBlade) > select **Start**. It takes a few minutes to complete the evaluation.

    > [!NOTE]
    >
    > - If you navigate away from the Migration evaluation, the only way to return is to open the [Migration evaluation](https://intune.microsoft.com/#blade/Microsoft_Intune_Workflows/MifoPolicyListBlade) link again.
    > - After you start the migration evaluation, you can't create new or edit existing device security policies in the Microsoft Defender portal.

3. Select **Recommendations**.

    This page displays the Intune policy recommendations based on your Basic Mobility and Security policies. The recommendations are read only and can't be changed.

    The name of each recommendation has a prefix based on the Basic Mobility and Security policy name. You need to review each item in the list, like the following example:

    :::image type="content" source="./media/migrate-to-intune/recommendations-page.png" alt-text="Screenshot of migration evaluation example in the Microsoft Intune admin center after migrating Microsoft 365 Basic Mobility and Security policies to Intune":::

    - Not all device settings correspond exactly to Intune settings and values. So, they can't be moved with precise one-to-one mapping. You need to review and possibly adjust these settings.
    - The Conditional Access (CA) settings that control the Office 365 services are the same CA policies in Microsoft Entra ID. So, you don't need to review or make changes to them unless you want to.

4. Select an item in the list. The **Compliance policy recommendation overview** page opens. Review the instructions.
5. Select **Details** to review the recommended settings and group assignments:

    :::image type="content" source="./media/migrate-to-intune/details-page.png" alt-text="Screenshot of details page example in the Microsoft Intune admin center after migrating Microsoft 365 Basic Mobility and Security policies to Intune":::

    The policy recommendations on this page are a read-only report documenting the suggested settings and assignments to use. They aren't Intune policies yet.

    While reviewing the recommendations, keep the following points in mind:

    - If the groups listed in the recommendation already have Intune policies assigned to them, then these policies may conflict with the recommended settings. To learn how conflicts are handled in Intune, go to [Common questions and answers with device policies and profiles in Microsoft Intune](../configuration/device-profile-troubleshoot.md#compliance-and-device-configuration-policies-that-conflict).

      > [!NOTE]
      > If you make any changes to migrated email profiles or fail to assign them to recommended groups, then users may be asked to re-enter their username and password to access email on their devices when the device migrates to Intune. For more information, go to [policy mapping for Configuration](policy-map-configurations.md).

    - If there are already Intune-licensed users in the recommended groups, then verify that the recommended policies are appropriate for these users. After you assign the policies to these groups, all Intune licensed users in the groups receive the policies, even users not previously managed by Basic Mobility and Security.

        > [!NOTE]
        > For the Windows operating system, only Windows 10/11 desktop devices will have policy migrated for them. Other versions of Windows won't have policy migrated. For more information, see the [Policy mapping for Access Requirements](policy-map-access-requirements.md) and [Policy mapping for Configuration](policy-map-configurations.md).

6. If you want to implement the recommended policy, then select **Open policy**. The policy page opens and the Intune policy is created. You can change or update the migrated policies.

    > [!NOTE]
    > If you delete the policy, the **Open policy** link from the recommendation page won't work.

At this point, the policy is created, but it's not doing anything yet. The next step is to assign the policy to the recommended groups or other groups you choose.

## Step 3 - Assign the policies and complete the migration

After the policies are created, they're ready to be assigned. For this migration to complete, all three have to be complete: assign groups, enable coexistence, and assign Intune licenses.

1. **Assign the recommended groups** to the policy. Select **Open policy** > **Properties** > **Edit** (next to **Assignments**) > use the assignments workflow to assign the groups.

    When you assign groups, your newly migrated Intune policies replace the device settings configured in Basic Mobility and Security. If you don't assign the groups, then devices managed by Basic Mobility and Security could lose settings and email configuration when their users are licensed for Intune. Remember, the Intune license assignment is a key step in the migration of devices from Basic Mobility and Security to Intune device management.

    For more information on the impact of existing Intune licenses, go to [Before you begin](#before-you-begin) (in this article).

2. **Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)** with Microsoft Entra **[License administrator](/entra/identity/role-based-access-control/permissions-reference#license-administrator)** rights.

3. **Enable [coexistence](mdm-authority-set.md#coexistence)**. When enabled:

    - Users with existing Intune licenses are immediately moved to Intune and the newly migrated policies are applied at the next [Intune refresh cycle](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals).
    - For users without Intune licenses, coexistence is the second step in the migration process. They'll be moved to Intune in the next step.

4. For users without Intune licenses, **assign Intune licenses** to the users you want to migrate. Your options:

    - Assign licenses to **Users**. For more information, go to [Assign licenses to users](/azure/active-directory/fundamentals/license-users-groups).
    - Assign licenses to **Groups**. For more information, go to [Assign licenses to a group](/azure/active-directory/enterprise-users/licensing-groups-assign).

    For more information on assigning licenses in Intune, go to [Assign licenses to users so they can enroll devices in Intune](licenses-assign.md).

At this point, the key steps are complete:

1. The policies are assigned to your groups.
2. Coexistence is enabled in Intune.
3. Intune licenses are assigned.

At the next [Intune device refresh cycle](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals), the devices automatically switch to Intune management and the new policies start affecting user devices.

## What did I just do?

This section describes what happens behind the scenes when you migrate from Basic Mobility and Security to Intune.

- The policies are mapped to Intune policies. For a mapping reference of the policies migrated by the **Migration evaluation**, go to:

  - [Access requirements policy mapping from Basic Mobility and Security to Intune](policy-map-access-requirements.md)
  - [Configurations policy mapping from Basic Mobility and Security to Intune](policy-map-configurations.md)
  - [Miscellaneous policy mapping from Basic Mobility and Security to Intune](policy-map-miscellaneous.md)

- When you complete the migration, your migrated policies are in Microsoft Intune admin center. The new policies include compliance policies, device configuration profiles, and Conditional Access policies. The new policies are in the following locations:

  | Intune policy type | Intune location |
  | --- | --- |
  | [Compliance policies](../protect/device-compliance-get-started.md)</br></br>Specify the device settings as access requirements. | [Microsoft Intune Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Compliance** |
  | [Configuration profiles](../configuration/device-profiles.md) </br></br> Specify other settings that aren't part of the access requirements, including email profiles. | [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Manage devices** > **Configuration** |
  | [Conditional Access policies]( ../protect/conditional-access.md)</br></br> Microsoft Entra Conditional Access blocks access if the settings aren't compliant. | [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Conditional Access** > **Classic policies** |

## Known issues

### Start button always appears

Each time you open the [Microsoft Intune admin center Migration evaluation](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/MifoPolicyListBlade), the **Start** button shows, even if the evaluation is already generated. If you dismiss the **Start** prompt, then the previously generated recommendations won't load.

**Workaround**: Start the evaluation again. It won't create more or duplicate recommendations or policies. Rerunning the migration detects that the evaluation has already succeeded and loads the previous recommendations.

### Number of sign-in failures before device is wiped setting isn't migrated

The **Number of sign-in failures before device is wiped** setting isn't migrated to Intune.

**Workaround**: If this setting was enabled in the Basic Mobility and Security policy, then this setting must be manually added to Intune device configuration profiles. For more information on the similar settings you can configure in Intune, go to:

- [Android Enterprise corporate-owned devices: Settings list to allow or restrict features](../configuration/device-restrictions-android-for-work.md)
- [Android Enterprise personally owned devices: Settings list to allow or restrict features](../configuration/device-restrictions-android-enterprise-personal.md)
- [iOS/iPadOS devices: Settings list to allow or restrict features](../configuration/device-restrictions-ios.md)
- [Windows 10/11 device: Settings list to allow or restrict features](../configuration/device-restrictions-windows-10.md)

## Next steps

- [What is Intune?](what-is-intune.md)
- [Get started with Intune](get-started-with-intune.md)
