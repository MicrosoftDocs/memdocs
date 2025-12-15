---
title: Windows Delivery Optimization settings in Microsoft Intune
description: Configure device configuration policy to manage Delivery Optimization settings on Windows devices you manage with Intune.
author: MandiOhlinger
ms.author: mandia
ms.date: 04/23/2025
ms.topic: how-to
ms.collection:
- M365-identity-device-management
ms.reviewer: juidaewo; davguy
---

# Delivery Optimization settings in Microsoft Intune

With Intune, you can use Delivery Optimization settings for your Windows devices to reduce bandwidth consumption when those devices download applications and updates. This article describes how to configure Delivery Optimization settings as part of an Intune device configuration profile. After you create a profile, you then assign or deploy that profile to your Windows devices.

> [!IMPORTANT]
> In April 2025, the settings format of the Delivery Optimization template was updated. Profiles for this new platform use the settings format as found in the Settings Catalog.  With this change you can no longer create new versions of the old profile. Your existing instances of the old profile remain available to use.
>
> For more information about this change, see the Intune Customer Success blog at [Support tip: Windows device configuration policies migrating to unified settings platform in Intune](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-windows-device-configuration-policies-migrating-to-unified-settings-/4189665).

- Learn about [Delivery Optimization updates](/windows/deployment/update/waas-delivery-optimization) in the Windows documentation.

This feature applies to:

- Windows

## Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New Policy**.

3. Enter the following properties:

   - **Platform**: Select **Windows 10 and later**.
   - **Profile type**: Select **Templates** > **Delivery Optimization**.

4. Select **Create**.

5. On the **Basics** page, enter the following properties:

   - **Name**: Enter a descriptive name for the new profile.
   - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. On the **Configuration settings** page, define how you want updates and apps to download. For information about the settings that are available in the template, drill in to the information icon and then select the *Learn more* link to view that settings Configuration Service Provider (CSP) details directly from Windows.

   When you're done configuring settings, select **Next**.

8. On the **Scope tags** page (optional), assign scope tags to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../intune-service/fundamentals/scope-tags.md).

   Select **Next** to continue.

9. On the **Assignments** page, select the groups that receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../intune-service/configuration/device-profile-assign.md).

   Select **Next**.

10. On the **Review + create** page, when you're done, choose **Create**. The profile is created and is shown in the list.

The next time each device checks in, the policy is applied.

## Next steps

- [Monitor the profiles status](device-profile-monitor.md).
- [Review available settings for the older profile format](../intune-service/configuration/delivery-optimization-settings.md). *Applies to profiles created before April 24, 2025*