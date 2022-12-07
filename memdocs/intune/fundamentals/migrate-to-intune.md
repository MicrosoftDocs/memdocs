---
# required metadata

title: Migrate from Microsoft 365 Basic Mobility and Security to Intune
titleSuffix: Microsoft Intune
description: Learn how to migrate your mobile device management from Microsoft 365 Basic Mobility and Security to Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 12/07/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Migrate from Microsoft 365 Basic Mobility and Security to Intune

Microsoft 365 includes a basic set of policies that protect devices and protect Microsoft 365 apps, like Outlook. These policies are managed in the Microsoft 365 Defender portal and are called **Basic Mobility and Security**. For more information on what Basic Mobility and Security offers, go to [Capabilities of Basic Mobility and Security](/microsoft-365/admin/basic-mobility-security/capabilities).

Many organizations want more device management features that are included with Microsoft Intune. For a comparison of the features, go [Choose between Basic Mobility and Security or Intune](/microsoft-365/admin/basic-mobility-security/choose-between-basic-mobility-and-security-and-intune).

You can migrate from Basic Mobility and Security to Microsoft Intune. Migrating to Intune requires the following three major steps:

1. **Prepare**: Review your Intune licenses, Basic Mobility and Security policies, group memberships, and devices to streamline the migration.
2. **Migrate policies**: Use the **Migration evaluation** in the [Endpoint Manager admin center](https://endpoint.microsoft.com/#view/Microsoft_Intune_Workflows/MifoPolicyListBlade). The output shows Intune policy and group recommendations that replace the Basic Mobility and Security policies.
3. **Migrate users and devices**: Assign licenses to users or groups, which will automatically switch the users to Intune device management at the next refresh cycle.

This article will help you migrate your mobile device management (MDM) from Microsoft 365 Basic Mobility and Security to Microsoft Intune.

## Before you begin

- Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with Azure AD Global or License administrator rights.

- Test the steps in this article on a group of test users who have devices enrolled in Basic Mobility and Security. Instead of assigning the actual suggested groups to the policy, assign a test group and confirm that the policies behave as expected.

- After you migrate to Intune, the existing device security policies deployed with Basic Mobility and Security are permanently frozen.

## Step 1 - Prepare

Before you migrate your Basic Mobility and Security policies, users and groups to Intune:

1. Be sure you have enough [Intune licenses](licenses.md) to cover all your users managed by Basic Mobility and Security.
2. Review the [device security policies](/microsoft-365/admin/basic-mobility-security/set-up#step-4-recommended-manage-device-security-policies) in the Microsoft 365 Defender portal. Delete any policies that are no longer needed. Deleting unneeded policies reduces the number of recommendations created by the Intune migration evaluation. So, you have fewer recommendations to review after the migration evaluation.
3. Review the [membership of groups](/microsoft-365/admin/basic-mobility-security/create-device-security-policies#step-3-deploy-a-policy-to-your-organization) that are currently assigned device security policies.

    - If these groups include users that are already licensed for Intune, then create new groups to separate Intune-licensed users from groups without Intune licenses.
    - Only assign Basic Mobility and Security device security policies to the users who aren't assigned Intune licenses.

4. Review the types of devices currently enrolled in Basic Mobility and Security. Unsupported [OS versions and variants](supported-devices-browsers.md#intune-supported-operating-systems) may continue to work, but they won’t be supported if migrated to Intune.

    For example, the settings applied to a Windows 8.1 Phone won’t be moved to Intune. If the user is licensed for Intune, their phone will lose any configuration set by device security policies in the Microsoft 365 Defender portal.

5. Before migration:

    - Don’t assign Intune licenses to users whose devices are managed by Basic Mobility and Security.
    - Don't assign Intune licenses to enable [app protection policies](../apps/app-protection-policy.md), also known as mobile application management (MAM).

    Only assign Intune licenses to users after the policy migration step is complete. The license assignment controls the migration of devices from Basic Mobility and Security to Intune. Before the first device is moved, make sure that sufficient Intune policies have been created to replace Basic Mobility and Security. For more information on a minimum base set of policies, go to [Get started with Intune](get-started-with-intune.md).

After the migration evaluation process activates, you can't make changes to your device security policies in the Microsoft 365 Defender portal. The existing Basic Mobility and Security policies are still enforced, but changes to these existing policies aren't saved.

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

## Step 2 - Migrate policies

After you’ve prepared your licenses and Basic Mobility and Security policies described in [Step 1 - Prepare](#step-1---prepare), you can use the **Migration evaluation** in the [Endpoint Manager admin center](https://endpoint.microsoft.com/#view/Microsoft_Intune_Workflows/MifoPolicyListBlade) to get Intune policy recommendations.

The tool can migrate your existing Basic Mobility and Security device security policies to Intune as [compliance policies](../protect/device-compliance-get-started.md) and [device configuration profiles](../configuration/device-profiles.md). It also makes recommendations for which groups they should be assigned.

These Intune recommendations are designed to replicate the Basic Mobility and Security policies. **You need to review these recommendations** to make sure that they reflect the old policies.

To evaluate and migrate policies from Basic Mobility and Security to Intune:

1. Complete the steps in the [Step 1 - Prepare](#prepare) section (in this article).
2. Open the [Migration evaluation](https://endpoint.microsoft.com/#blade/Microsoft_Intune_Workflows/MifoPolicyListBlade) > select **Start**. It will take a few minutes to complete the evaluation.

    > [!NOTE]
    > 
    > - If you navigate away from the Migration evaluation, the only way to return is to open the [Migration evaluation](https://endpoint.microsoft.com/#blade/Microsoft_Intune_Workflows/MifoPolicyListBlade) link again.
    > - After you start the migration evaluation, you can't create new or edit existing device security policies in the Microsoft 365 Defender portal.

3. Select **Recommendations**. This page displays the Intune policy recommendations based on your Basic Mobility and Security policies. The recommendations are read only and won’t change. The name of each recommendation has a prefix based on the Basic Mobility and Security policy name. You need to review each item in the list, like the following example:

    :::image type="content" source="./media/migrate-to-intune/recommendations-page.png" alt-text="Screenshot of migration evaluation example in the Endpoint Manager admin center after migrating Microsoft 365 Basic Mobility and Security policies to Intune":::

    - You won’t need to review or make changes to the settings controlling conditional access to Office 365 services. They’re backed by classic Azure Active Directory conditional access policies and are directly available through the Azure AD portal. These policies are exactly the same underlying policies managed indirectly through the device security policies in the Microsoft 365 Defender portal. So, there’s no need to review or change them.
    - Not all device settings offered in device security policies correspond exactly to Intune settings and values. Therefore, they can’t be moved with precise one-to-one mapping. You need to review and possibly adjust these settings.

4. Select an item in the list. The **Compliance policy recommendation overview** page opens. Review the instructions.
5. Select **Details** to review the recommended settings and group assignments:

    :::image type="content" source="./media/migrate-to-intune/details-page.png" alt-text="Screenshot of details page example in the Endpoint Manager admin center after migrating Microsoft 365 Basic Mobility and Security policies to Intune":::

    The policy recommendations on this page aren't an Intune policy yet. It’s a read-only report documenting the suggested settings and assignments to use. While reviewing the recommendations, keep these points in mind:

    - If the groups listed in the recommendation already have Intune policies assigned to them, then these policies may conflict with the recommended settings. To learn how conflicts are handled in Intune, go to [Common questions and answers with device policies and profiles in Microsoft Intune](../configuration/device-profile-troubleshoot.md#if-multiple-policies-are-assigned-to-the-same-user-or-device-how-do-i-know-which-settings-gets-applied).

      > [!NOTE]
      > If you make any changes to migrated email profiles or fail to assign them to recommended groups, then users may be asked to re-enter their username and password to access email on their devices when the device migrates to Intune. For more information, go to [policy mapping for Configuration](policy-map-configurations.md).

    - If there are already Intune-licensed users in the recommended groups, then verify that the recommended policies are appropriate for these users. After you assign the policies to these groups, all Intune licensed users receive the policies, even users not previously managed by Basic Mobility and Security.

    > [!NOTE]
    > For the Windows operating system, only Windows 10/11 desktop devices will have policy migrated for them. Other versions of Windows won't have policy migrated. For more information, see the [Policy mapping for Access Requirements](policy-map-access-requirements.md) and [Policy mapping for Configuration](policy-map-configurations.md).

6. If you want to implement the recommended policy, then select **Open policy**. The policy page opens.

    - In this page, the policy is in draft mode and you can change or update the migrated policies.
    - The policy doesn’t have any groups assigned to it yet. So, it’s not affecting any users who are licensed for Intune and who are in the same groups assigned to the original device security policy.

      Now, the policy is ready to be assigned to the recommended groups or to other groups.

    > [!NOTE]
    > If you delete the policy, the **Open policy** link from the recommendation page won’t work.

7. To assign the recommended groups to the policy, select **Properties** > **Edit** (next to **Assignments**) > use the assignments workflow to assign the groups.

    When you assign, your newly migrated Intune policies replace the device settings configured in Basic Mobility and Security. If you don’t assign the groups, then devices managed by Basic Mobility and Security could lose settings and email configuration when their users are licensed for Intune. Remember, the Intune license assignment controls the migration of devices from Basic Mobility and Security to Intune.

    Devices managed by the Basic Mobility and Security will migrate after you assign Intune licenses to the users at the next [Intune refresh cycle](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

8. Enable [coexistence](mdm-authority-set.md#coexistence). After you enable coexistence, all users that have an Intune license or get assigned an Intune license immediately migrate to Intune.
9. Assign Intune [licenses](/azure/active-directory/fundamentals/license-users-groups) to the user groups that don't have Intune licenses. The new policies will begin affecting the users' devices after the next [Intune refresh cycle](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## Step 3 - Migrate users and devices

To migrate a user and their devices from Basic Mobility and Security to Intune:

1. Enable [coexistence](mdm-authority-set.md#coexistence). Enabling coexistence will immediately migrate all devices whose users are assigned an Intune license.
2. Sign in to the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with Azure AD Global or License administrator rights.
3. Assign Intune licenses to the users you want to migrate by using users or groups:

    - Assign licenses to **Users**. For more information, see [Assign licenses to users](/azure/active-directory/fundamentals/license-users-groups).
    - Assign licenses to **Groups**. For more information, see [Assign licenses to a group](/azure/active-directory/enterprise-users/licensing-groups-assign).

4. After a user is licensed for Intune, their devices will automatically switch to Intune management at the next device refresh cycle. See [Refresh cycles](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## After the migration

For a mapping reference of the policies migrated by the **Migration evaluation**, go to the following articles:

- [Access requirements policy mapping from Basic Mobility and Security to Intune](policy-map-access-requirements.md)
- [Configurations policy mapping from Basic Mobility and Security to Intune](policy-map-configurations.md)
- [Miscellaneous policy mapping from Basic Mobility and Security to Intune](policy-map-miscellaneous.md)

When you complete the migration, you'll find your migrated policies in Microsoft Endpoint Manager admin center in the following locations:

| Intune policy type | Intune location |
| --- | --- |
| [Compliance policies](../protect/device-compliance-get-started.md)</br></br>Specify the device settings as access requirements. | [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Compliance policies** |
| [Configuration profiles](../configuration/device-profiles.md) </br></br> Specify other settings that aren’t part of the access requirements, including email profiles. | [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Configuration profiles** |
| [Conditional access policies]( ../protect/conditional-access.md)</br></br> Azure AD conditional access blocks access if the settings aren't compliant. | [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Conditional access** > **Classic policies** |

## Known issues

### Start button always appears

The **Start** button will appear each time you open the Migration evaluation page, even if the evaluation is already generated. If you dismiss the **Start** prompt, the previously generated recommendations won’t load.

**Workaround**: Start the evaluation again. It won’t create more or duplicate recommendations or policies. Rerunning the migration detects that the evaluation has already succeeded and loads the previous recommendations.

### Number of sign-in failures before device is wiped setting isn’t migrated

The **Number of sign-in failures before device is wiped** setting isn’t migrated to Intune. 

**Workaround**: This setting must be manually added to Intune device configuration profiles if it was enabled in the Basic Mobility and Security policy.

## Next steps

[What is Intune?](what-is-intune.md)
